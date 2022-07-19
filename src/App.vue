<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h1>Todo application</h1>
    <hr>
    <!-- <AddTodo @add-todo="addTodo"></AddTodo> -->
    <select name="" id="" v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="no-completed">No Completed</option>
    </select>
    <hr>
    <div class="select-box">
      <!-- <SelectForm :select="options[3]" :options="options" :showCheckbox="showCheckbox" @checkbox-checked="toggleChecked"
        @select="optionSelect"/> -->
      <ProcessSelection :select="options[0]" :options="options" :showCheckbox="showCheckbox"
        @checkbox-checked="toggleChecked" @select="optionSelect" />
    </div>

    <LoaderList v-if="loading" />
    <!-- <TodoList v-else-if="todos.length" v-bind:todos="filteredTodos" v-on:remove-todo="removeTodo" /> -->
    <!-- <p v-else>No todos</p> -->
    <hr>
    <!-- <CustomSelect :options="options" @select="optionSelect" :selected="selected" /> -->
  </div>
</template>

<script>

// import HelloWorld from './components/HelloWorld.vue';
// import TodoList from '@/components/TodoList.vue';
// import AddTodo from '@/components/AddTodo.vue';
import LoaderList from '@/components/LoaderList.vue';
// import SelectForm from '@/components/SelectForm.vue';
// import CustomSelect from '@/components/CustomSelect.vue';
// import ProcessSelection from '@/components/custom-select/ProcessSelection.vue';
import ProcessSelection from '@/components/ProcessSelection.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
      options: [
        { id: 1, label: 'Accepted', color: '#04ff00',  checked: false },
        { id: 2, label: 'In process', color: '#fff700', checked: true },
        { id: 3, label: 'Rejected', color: '#ff1100',  checked: false },
        { id: 4, label: 'Postponed', color: '#00fffb', checked: true },
        { id: 5, label: 'Returned', color: '#0015ff', checked: false },
      ],
      showCheckbox: true,
      selectedId: '',
      selected: { id: 1, label: 'To buy a chief', color: '#ff1100', checked: false },
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
    optionSelect(option) {
      this.selectedId = option.id;
    },
    customOptionSelect(option) {
      this.selected = option;
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
    // TodoList,
    // AddTodo,
    LoaderList,
    // SelectForm,
    // CustomSelect,
    ProcessSelection,
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

.select-box {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
</style>
