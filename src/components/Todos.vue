<template>
  <div>
    <TodoItemComponent v-for="task in todoList" v-bind:key="task" v-bind:todoProps="task" />
  </div>
</template>

<script>
import { ref } from 'vue'
import TodoItemComponent from './TodoItem.vue'

export default {
  name: 'Todos-component',
  components: { TodoItemComponent },
  //setup(): pass all data to the template, including all data of component
  setup() {
    const todos = ref(['task 1', 'task 2', 'task 3'])
    return { todoList: todos }
  }
}
</script>

<style></style>
