<template>
  <div>
    <TodoItemComponent
      v-for="task in todoList"
      v-bind:key="task.id"
      v-bind:todoProps="task"
      v-on:check-task="checkTodoTask"
    />
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
    //ref: start initial data/ state
    const todos = ref([
      {
        id: 1,
        title: 'task 1',
        isCompleted: false
      },
      {
        id: 2,
        title: 'task 2',
        isCompleted: false
      },
      {
        id: 3,
        title: 'task 3',
        isCompleted: false
      }
    ])

    const checkTodoTask = (id) => {
      // console.log('task id received from child component', id)
      // console.log('todos', todos)
      todos.value = todos.value.map((task) => {
        if (task.id === id) task.isCompleted = !task.isCompleted
        return task
      })
    }
    return { todoList: todos, checkTodoTask }
  }
}
</script>

<style></style>
