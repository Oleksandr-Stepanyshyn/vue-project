<template>
  <li>
    <span v-bind:class="{done: toggle || todo.completed}">
      <input type="checkbox" v-model="toggle" v-bind:checked="todo.completed">
      <strong>{{index + 1}}</strong>
      {{todo.title.toUpperCase()}}
    </span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true
    },
  },
  data() {
    return {
      toggle: false,
    }
  },
  methods: {
    changeText() {
      console.log()
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 2rem;
  }

  .rm {
    background-color: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
  }

  input {
    margin-right: 1rem;
  }

  .done{
    text-decoration: line-through;
  }
</style>