<script setup lang="ts">
import { ref } from 'vue'

// defining types
type todoItem = {
  id: number,
  text: string
}

// give each todo a unique id
let id: number = 0

// we used ref because it's a simple, no need to use reactive.
const newTodo = ref<string>('')
const todos = ref<todoItem[]>([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo(): void {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo: todoItem): void {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
