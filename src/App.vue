<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <b-jumbotron>
            <TodoList :todos="todos" :completed="completed" :deleteTodo="deleteTodo" />
            <br />
            <AddTodo :addTodo="addTodo" />
          </b-jumbotron>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import TodoList from "./components/TodoList.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "app",
  components: {
    Header,
    TodoList,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async listTodo() {
      await fetch("http://localhost:4500/api/todo/list", { method: "get" })
        .then(response => response.json())
        .then(data => {
          this.todos = data;
        });
    },
    async addTodo(todo) {
      let newTodo = { completed: false, text: todo };
      await fetch("http://localhost:4500/api/todo/add", {
        method: "post",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(newTodo)
      }).then(response => {
        this.listTodo();
      });
    },
    async completed(todo) {
      if (todo) {
        todo.completed = !todo.completed;
        await fetch(`http://localhost:4500/api/todo/todos/${todo._id}`, {
          method: "put",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(todo)
        }).then(response => {
          //  console.log(response && response.status)
        });
      }
    },
    async deleteTodo(todo) {
      if (todo) {
        await fetch(`http://localhost:4500/api/todo/todos/${todo._id}`, {
          method: "delete",
          headers: { "Content-Type": "application/json" }
        }).then(response => {
          this.listTodo();
        });
      }
    }
  },
  mounted() {
    this.listTodo();
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
