<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h1>Todo application</h1>
    <hr>
    <AddTodo @add-todo="addTodo"></AddTodo>
    <select name="" id="" v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="no-completed">No Completed</option>
    </select>
    <hr>
    <SelectForm 
      :select="options[3]" 
      :options="options" 
      :showCheckbox="showCheckbox" 
      @checkbox-checked="toggleChecked" 
      @select="selected">
    </SelectForm>
    <LoaderList v-if="loading" />
    <TodoList v-else-if="todos.length" v-bind:todos="filteredTodos" v-on:remove-todo="removeTodo" />
    <p v-else>No todos</p>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TodoList from '@/components/TodoList.vue'
import AddTodo from '@/components/AddTodo.vue'
import LoaderList from '@/components/LoaderList.vue'
import SelectForm from '@/components/SelectForm.vue'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
      options: [
        { id: 1, label: 'To buy a chief', color: '#ff1100', checked: false },
        { id: 2, label: 'To buy a car', color: '#fff700', checked: true },
        { id: 3, label: 'To buy a beer', color: '#04ff00', checked: false },
        { id: 4, label: 'To buy a lamp', color: '#00fffb', checked: true },
        { id: 5, label: 'To buy a chair', color: '#0015ff', checked: false },
      ],
      showCheckbox: true,
      selectedId: '',
    }
  },

  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=4')
      .then(response => response.json())
      .then(json => {
        this.todos = json;
        this.loading = false
      })
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      if (this.filter === "completed") {
        return this.todos.filter(todo=>todo.completed)
      }
      if (this.filter === "no-completed") {
        return this.todos.filter(todo => !todo.completed)
      }
    return this.todos
    }
  },
  methods: {
    selected(id) {
      this.selectedId = id;
    },
    toggleChecked(checked) {
      this.options.forEach(opt => {
        if (opt.id === this.selectedId) {
          opt.checked = checked;
          return;
        }
      })
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo=>todo.id !== id)
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    }
  },
  components: {
    // HelloWorld
    TodoList,
    AddTodo,
    LoaderList,
    SelectForm,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
