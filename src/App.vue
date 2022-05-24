<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center mb-40">Todo App</h1>
      <input type="text" class="form-control mb-40" v-model="userInput" @keyup.enter="addNewTodos">
      <div class="list-group">
        <button class="list-group-item text-left" @click="toggleTodoState(todo)" v-for="(todo, idx) in activeTodoList " :key="idx">{{todo.label}}</button>
      </div>
      <div class="text-right">
        <button class="btn btn-sm" @click="changeCurrentState('active')">Todo</button>
        <button class="btn btn-sm" @click="changeCurrentState('done')">Done</button>
        <button class="btn btn-sm" @click="changeCurrentState('all')">Entire</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      userInput: "",
      todoList: [],
      currentState: 'active',
    }
  },
  computed: {
    activeTodoList() {
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState)
    },
  },
  methods: {
    changeCurrentState(state) {
      this.currentState = state
    },
    addNewTodos() {
      this.todoList.push({
        label: this.userInput,
        state: 'active',
      })
      this.userInput = ''
    },
    toggleTodoState(todo) {
      todo.state = todo.state === 'active' ? 'done' : 'active'
    }
  },
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
