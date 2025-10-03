<script setup>
import { ref } from 'vue'

const list = ref([
  { text: 'Köp mjölk', done: false },
  { text: 'Köp ägg', done: true },
  { text: 'Köp bröd', done: false },
])
const itemText = ref('')
function addItem() {
  let listItem = { text: itemText.value, done: false }
  list.value.push(listItem)
  itemText.value = ''
}
function radera(listItem) {
  list.value = list.value.filter((obj) => {
    return obj !== listItem
  })
}
</script>

<template>
  <header>
    <h1>Todo-lista</h1>
    <input type="text" v-model="itemText" placeholder="Ny uppgift" />
    <button v-on:click="addItem">Lägg till</button>
  </header>

  <main>
    <h3 id="todo">Att göra:</h3>
    <ul>
      <template v-for="itm in list" v-bind:key="itm">
        <li v-if="!itm.done" @click="itm.done = !itm.done" class="todoItm">
          {{ itm.text }}<span title="Radera" @click="radera(itm)">❌</span>
        </li>
      </template>
    </ul>
    <h3 id="klart">Klart!</h3>
    <ul>
      <template v-for="itm in list" v-bind:key="itm">
        <li v-if="itm.done" @click="itm.done = !itm.done" class="todoItm done">
          {{ itm.text }}<span title="Radera" @click="radera(itm)">❌</span>
        </li>
      </template>
    </ul>
  </main>
</template>

<style scoped>
.todoItm {
  font-weight: bold;
  padding: 0.5em;
  list-style-type: none;
  cursor: pointer;
}
.todoItm:nth-child(odd) {
  background-color: lightblue;
}
.todoItm:nth-child(even) {
  background-color: lightgreen;
}
.done {
  text-decoration: line-through solid black;
}
#klart {
  color: greenyellow;
}
#todo {
  color: red;
}
li span {
  display: inline-block;
  position: absolute;
  right: 3em;
  background-color: white;
  padding-left: 0.5em;
  padding-right: 0.5em;
}
</style>
