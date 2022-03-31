<template>
  <div>
    <AddTodo @add-todo="AddTodo" />
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todoProps="todo"
      @item-completed="markItem"
      @delete-item="deleteTodo"
    ></TodoItem>
  </div>
</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
import axios from 'axios'

export default {
  name: 'todo-component',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])

    const getTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=10'
        )
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getTodos()
    const markItem = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }
    const deleteTodo = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter((todo) => todo.id !== id)
      } catch (error) {
        console.log(error)
      }
    }
    const AddTodo = async (newTodo) => {
      try {
        const ref = await axios.post(
          `https://jsonplaceholder.typicode.com/todos`,
          newTodo
        )
        todos.value.push(ref.data)
      } catch (error) {
        console.log(error)
      }
    }
    return {
      todos,
      markItem,
      deleteTodo,
      AddTodo
    }
  }
}
</script>

<style>
</style>