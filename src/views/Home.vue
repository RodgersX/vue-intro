<template>
  <div id="app">
    <Header />
    <AddTodo @add-todo="addTodo"/>
    <todos :todos="todos" @del-todo="deleteTodo"/>
  </div>
</template>

<script>
import todos from '../components/todos'
import AddTodo from '../components/addTodo'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    todos,
    AddTodo
  },

  data() {
    return {
      todos: []
    }
  },

  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos')
      .then(res => this.todos = res.data)
      //.catch(err)
  },

  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      //this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, completed
      })
      .then(res => {
        this.todos = [...this.todos, res.data]
      })
      //this.todos = [...this.todos, newTodo]
    }
},
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
