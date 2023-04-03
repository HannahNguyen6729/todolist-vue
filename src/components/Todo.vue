<template>
  <div>
    <div v-for="task in todoList" v-bind:key="task">
      {{ task }}
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Todos-component',
  //setup(): pass all data to the template, including all data of component
  setup() {
    const todos = ref(['task 1', 'task 2', 'task 3'])
    return { todoList: todos }
  }
}
</script>

<style></style>
