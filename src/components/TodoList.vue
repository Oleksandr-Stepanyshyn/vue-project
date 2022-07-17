<template>
  <div class="todo__list">
    <ul>
      <TodoItem 
        v-for="(todo, idx) in todos" 
        :key="todo.id"
        v-bind:todo="todo"
        v-bind:index="idx"
        v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
  props:['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id)
    }
  }
}
</script>

<style scoped>
.todo__list{
  margin-top: 12px;
}
ul{
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>