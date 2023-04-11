<script setup>
  import { computed, ref } from "vue";

  const todoList = ref([])

  const completedItems = computed(() => {
      return todoList.value.filter(item => item.completed)
    })
  const remainingItems = computed(() => {
      return todoList.value.filter(item => !item.completed)
  })

  function fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos/')
      .then(response => response.json())
      .then(json => {todoList.value = json})
    }

</script>
<template>
    <img src="/todo.jpg" alt="Todo photo"/>
    <h1>Hello world! :)</h1>
    <button @click="fetchTodoList">Fetch Data</button>
    <p>{{completedItems.length}} completed | {{remainingItems.length}} remaining</p>
    <ul v-for="todo in todoList" :key="`todo-id-${todo.userId}`">
      <input type="checkbox" :checked="todo.completed"/>
      <li>{{todo}}</li>
    </ul>
</template>