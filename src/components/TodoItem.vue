<template>
  <div :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todoProps.completed" v-on:change="markItem"/>
    {{ todoProps.title }}
    <button class="btn" @click="deleteItem">delete</button>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'todo-component',
  props: ['todoProps'],
  setup(props, context) {
    const id = ref('my-id2')
    const markItem = () => {
      context.emit('item-completed', props.todoProps.id)
    }
    const deleteItem = () => {
      context.emit('delete-item', props.todoProps.id)
    }
    return {
      id,
      markItem,
      deleteItem
    }
  }
}
</script>

<style>
.btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}
.todo-item {
  background: #fff;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
.is-completed {
  text-decoration: line-through;
}
</style>