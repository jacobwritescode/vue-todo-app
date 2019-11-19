<template>
  <div>
    <b-container class="bv-example-row">
      <form v-on:submit.prevent="AddTodo">
        <b-row>
          <b-col>
            <b-form-input v-model="todo" placeholder="Write your todo here"></b-form-input>
          </b-col>
          <b-button variant="success" @click="AddTodo">Add</b-button>
        </b-row>
      </form>
    </b-container>
  </div>
</template>
<script>
export default {
  name: "AddTodo",
  props: {
    addTodo: Function
  },
  data() {
    return {
      todo: ""
    };
  },
  methods: {
    AddTodo() {
      this.addTodo(this.todo);
      this.todo = "";
    }
  }
};
</script>