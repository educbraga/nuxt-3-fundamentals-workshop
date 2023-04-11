<script>
  import { defineNuxtComponent } from '#app'
export default defineNuxtComponent ({
  data: () => ({
    todoList: []
  }),
  computed: {
    completedItems() {
      return this.todoList.filter(item => item.completed)
    },
    remainingItems() {
      return this.todoList.filter(item => !item.completed)
    }
  },
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos/')
      .then(response => response.json())
      .then(json => {this.todoList = json})
    }
  } 
})
</script>
<template>
  <div>
    <img src="/todo.jpg" alt="Todo photo"/>
    <h1>Hello world! :)</h1>
    <button @click="fetchTodoList">Fetch Data</button>
    <p>{{completedItems.length}} completed | {{remainingItems.length}} remaining</p>
    <ul v-for="todo in todoList" :key="`todo-id-${todo.userId}`">
      <input type="checkbox" :checked="todo.completed"/>
      <li>{{todo}}</li>
    </ul>
  </div>
</template>