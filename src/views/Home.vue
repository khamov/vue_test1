<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    {{msg}}
    <!--<Header/> -->
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
// import Header from './../layout/Header';
import Todos from './../components/Todos';
import AddTodo from './../components/AddTodo';
import axios from 'axios';
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    //Header,
    Todos,
    AddTodo
    // HelloWorld
  },
  data() {
    return {
      msg: 'Hello from Alex',
      todos: [
        /*
        {
          id:1,
          title: "One",
          completed: false,
        },
        {
          id:2,
          title: "Two",
          completed: false,
        }
        */
      ]
    };
  },
  methods: {
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter((todo) => todo.id !== id));
      //this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      // this.todos = [...this.todos, newTodo];
    },
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data);
    //.catch(err => console.log(err));
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
