<template>
  <div class="todo-item is-completed" id="">
    <input type="checkbox" />
    {{ todoProps.title }}
    <button class="btn" type="submit">delete</button>
  </div>
</template>

<script>
export default {
  name: 'todo-component',
  props: ['todoProps']
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