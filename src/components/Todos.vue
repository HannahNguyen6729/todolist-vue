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
//import { v4 as uuidv4 } from 'uuid'
import axios from 'axios'
import TodoItemComponent from './TodoItem.vue'
import AddTodoComponent from './AddTodo.vue'

export default {
  name: 'Todos-component',
  components: { TodoItemComponent, AddTodoComponent },
  //setup(): pass all data to the template, including all data of component
  setup() {
    //ref: start initial data/ state
    // const todos = ref([
    //   {
    //     id: uuidv4(),
    //     title: 'task 1',
    //     isCompleted: false
    //   },
    //   {
    //     id: uuidv4(),
    //     title: 'task 2',
    //     isCompleted: false
    //   },
    //   {
    //     id: uuidv4(),
    //     title: 'task 3',
    //     isCompleted: false
    //   }
    // ])

    const todos = ref([])
    const getAllTasks = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        todos.value = res.data
      } catch (err) {
        console.log(err)
      }
    }
    getAllTasks()

    const checkTodoTask = (id) => {
      // console.log('task id received from child component', id)
      // console.log('todos', todos)
      todos.value = todos.value.map((task) => {
        if (task.id === id) task.completed = !task.completed
        return task
      })
    }

    const addTodo = async (newTask) => {
      try {
        // console.log('newTask', newTask)
        // console.log('todos.value', todos.value)
        const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTask)
        //console.log(res.data)
        todos.value.push(res.data)
      } catch (e) {
        console.log(e)
      }
    }

    const deleteTodoItem = async (id) => {
      try {
        // console.log('todo item id received from child component', id)
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter((task) => task.id !== id)
      } catch (err) {
        console.log(err)
      }
    }
    return { todoList: todos, checkTodoTask, deleteTodoItem, addTodo }
  }
}
</script>

<style></style>
