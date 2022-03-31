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
import { v4 as uuidv4 } from 'uuid'

export default {
  name: 'todo-component',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([
      {
        id: uuidv4(),
        title: 'viec 1',
        completed: false
      },
      {
        id: uuidv4(),
        title: 'viec 2',
        completed: false
      },
      {
        id: uuidv4(),
        title: 'viec 3',
        completed: false
      }
    ])
    const markItem = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed
        return todo
      })
    }
    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => todo.id !== id)
    }
    const AddTodo = (newTodo) => {
      todos.value.push(newTodo)
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