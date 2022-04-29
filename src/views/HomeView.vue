<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <TodoItem v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import TodoItem from "../components/TodoItem.vue";
import AddTodo from "../components/AddTodo.vue";
import axios from 'axios';


export default {
  name: "HomeView",
  components: {
    TodoItem,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    // deleteTodo(id) {
    //   this.todos = this.todos.filter((todo) => todo.id !== id);
    // },
    // addTodo(newTodo){
    //   this.todos = [...this.todos,newTodo];
    // }
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          () => (this.todos = this.todos.filter((todo) => todo.id !== id))
        )
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 2.4d;
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
