<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row class="mt-5 text-center">
        <b-col>
          <h1 class="main-title text-light">k+k Todos</h1>
        </b-col>
      </b-row>
      <b-row class="mt-5 text-center">
        <b-col>
          <AddTodo @todo-added="handleTodoAdded"></AddTodo>
        </b-col>
      </b-row>
      <b-row class="mt-3">
        <b-col>
          <div class="controls text-center" v-if="todos.length > 0 ">
            <b-button variant="success" size="sm" class="mx-3" @click="markAllTodosCompleted">Mark All Completed</b-button>
            <b-button variant="warning" size="sm" class="mx-3" @click="deleteAllTodos">Delete All</b-button>
          </div>
          <TodosList :todos="this.todos" @todo-deleted="handleTodoDeleted"></TodosList>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo";
import TodosList from "@/components/TodosList";

export default {
  name: "App",
  components: {
    TodosList,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    handleTodoAdded: function(newTodo) {
      this.todos.push(newTodo);
    },
    handleTodoDeleted: function(todo) {
      this.todos = this.todos.filter(item => item != todo);
    },
    deleteAllTodos: function() {
      this.todos = []
    },
    markAllTodosCompleted: function() {
      this.todos.map(item => 
        item.completed = true
      )
    },
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("todos"))
      this.todos = JSON.parse(localStorage.getItem("todos"));
  }
};
</script>

<style lang="scss">
</style>
