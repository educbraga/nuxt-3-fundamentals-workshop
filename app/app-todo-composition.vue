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
    <p class="heading">todo photo!</p>
    <h1 class="title">Hello world! :)</h1>
    <button @click="fetchTodoList">Fetch Data</button>
    <p>{{completedItems.length}} completed | {{remainingItems.length}} remaining</p>
    <ul class="list" v-for="todo in todoList" :key="`todo-id-${todo.userId}`">
      <li ><input type="checkbox" :checked="todo.completed"/> {{todo.title}}</li>
    </ul>
</template>
<style lang="scss">
  @import './node_modules/bulma/bulma.sass';
  @import './assets/styles/main.scss';

  :root {
    --text-color: #{$text-color};
  }

  .heading {
    color: var(--text-color);
  }
  .list {
    color: var(--text-color);
  }
</style>