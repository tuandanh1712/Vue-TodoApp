<template>
  <div class="todo">
    <Header></Header>
    <AddTodo @add-todo="addTodo"></AddTodo>
    <todos :todos="todos" @del-todo="deleteTodo"></todos>
  </div>
</template>

<script>
import AddTodo from "./components/AddTodo.vue";
import Header from "./components/layout/Header.vue";
import Todos from "./components/Todos.vue";
import axios from "axios";

export default {
  components: { Header, AddTodo, Todos },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
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
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>
<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  display: block;
}
#app {
  max-width: 100%;
  padding: 0;
  margin: 0;
  display: block;
}
</style>
