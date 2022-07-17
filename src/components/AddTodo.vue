<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title">
    <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title:' '
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: this.title.length,
          title: this.title,
          completed: false
        }
        this.$emit('add-todo', newTodo)
        this.title=''
        }
      }
    }
  }
</script>

<style scoped>
form {
  display: flex;
  align-items: center;
  justify-content: center;

}

input {
  width: 320px;
}
</style>