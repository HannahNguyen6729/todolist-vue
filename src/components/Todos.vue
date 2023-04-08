<template>
  <div>
    <AddTodoComponent @add-todo="addTodo" />
    <TodoItemComponent
      v-for="task in todoList"
      :key="task.id"
      :todoProps="task"
      @check-task="checkTodoTask"
      @delete-item="deleteTodoItem"
    />
  </div>
</template>

<script>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'
import TodoItemComponent from './TodoItem.vue'
import AddTodoComponent from './AddTodo.vue'

export default {
  name: 'Todos-component',
  components: { TodoItemComponent, AddTodoComponent },
  //setup(): pass all data to the template, including all data of component
  setup() {
    //ref: start initial data/ state
    const todos = ref([
      {
        id: uuidv4(),
        title: 'task 1',
        isCompleted: false
      },
      {
        id: uuidv4(),
        title: 'task 2',
        isCompleted: false
      },
      {
        id: uuidv4(),
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

    const addTodo = (newTask) => {
      // console.log('newTask', newTask)
      // console.log('todos.value', todos.value)
      todos.value.push(newTask)
    }

    const deleteTodoItem = (id) => {
      // console.log('todo item id received from child component', id)
      todos.value = todos.value.filter((task) => task.id !== id)
    }
    return { todoList: todos, checkTodoTask, deleteTodoItem, addTodo }
  }
}
</script>

<style></style>
