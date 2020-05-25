<template>
  <div id="app">
    <!-- <Header /> -->
    <AddTodo v-on:add-todo="addTodo" />
   <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  
  </div>
</template>

<script>
// import Header from '../components/layout/Header.vue'
import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    // Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://my-json-server.typicode.com/sarangaranaweera/jsonplaceholder/todos/${id}`)
      // eslint-disable-next-line no-unused-vars
      .then( res => this.todos = this.todos.filter(todo => todo.id !== id ))
      .catch(err => console.log(err));

    },
    addTodo(newTodo) {
      const {title,completed} = newTodo;

      axios.post('https://my-json-server.typicode.com/sarangaranaweera/jsonplaceholder/todos',{
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(error => console.log(error))
     
    }
    
  },
  created() {
      axios.get('https://my-json-server.typicode.com/sarangaranaweera/jsonplaceholder/todos')
      .then(res => this.todos = res.data)
      .catch(error => console.log(error))
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
}
</style>