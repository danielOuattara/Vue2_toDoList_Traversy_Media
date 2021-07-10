<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addToTodos"/>
    <Todos :todos='todos' v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>

import Header  from './components/layout/Header.vue';
import Todos   from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import axios   from 'axios';

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },

  data() {
    return {
//      todos:[
//        { id: 1, title: "Todo One", completed: false },
//        { id: 2, title: "Todo Two", completed: true },
//        { id: 3, title: "Todo Three", completed: false },
//      ],
        todos: [],
    }
  },

  methods: {

    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then( (/*res*/) => this.todos = this.todos.filter( todo => todo.id !== id ) )
      .catch(err => console.log(err));
    },

    addToTodos(newTodo) {
      const {title, completed} = newTodo;
      this.todos = [...this.todos, newTodo];
      axios.post('https://jsonplaceholder.typicode.com/todos', {title, completed })
      .then( res => this.todos = [...this.todos, res.data] )
      .catch(err => console.log(err));
    },
  },

  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit= 5')
    .then( res => this.todos = res.data )
    .catch(err => console.log(err));
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.4
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
  border: #333;
  padding: 4px 17px;
  border:3px solid #000
}






</style>
