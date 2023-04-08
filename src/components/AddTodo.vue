<template>
  <form @submit="handleAddTodo">
    <input v-model="title" @input="handleInputChange" type="text" placeholder="enter task..." />
    <button type="submit" class="add-btn">Add</button>
  </form>
</template>
<script>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

export default {
  name: 'AddTodoComponent',
  setup(props, context) {
    const title = ref('')

    const handleInputChange = () => {
      console.log('input value after changing', title.value)
    }

    const handleAddTodo = (event) => {
      event.preventDefault()
      const newTask = {
        id: uuidv4(),
        title: title.value,
        isCompleted: false
      }
      context.emit('add-todo', newTask)
      title.value = ''
    }

    return { handleInputChange, title, handleAddTodo }
  }
}
</script>
<style scoped>
form {
  display: flex;
  padding: 10px;
}
input[type='text'] {
  width: 100%;
  height: 20px;
}
.add-btn {
  background-color: aquamarine;
  border: none;
  border-radius: 5px;
  padding: 5px 20px;
  margin-left: 10px;
  cursor: pointer;
}
</style>
