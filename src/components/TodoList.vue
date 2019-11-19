<template>
  <div class="question-box-container">
    <b-list-group>
      <b-list-group-item v-for="(todo,index) in todos" :key="index">
        <b-row>
          <b-col>{{todo.text}}</b-col>
          <b-col>
            <b-button
              @click="completed(todo)"
              :variant="todo.completed ? 'success' : 'outline-primary'"
            >{{todo.completed ? "Completed" :"Yet to Finish"}}</b-button>
            <b-button @click="deleteTodo(todo)">Delete</b-button>
          </b-col>
        </b-row>
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todos: Array,
    completed: Function,
    deleteTodo: Function
  }
};
</script>