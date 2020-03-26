<template>
  <div class="add-todo">
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        class="add-todo-input"
        placeholder="Add a todo..."
        autofocus
        autocomplete="off"
      />
      <b-button type="submit" class="add-todo-btn" variant="success" v-if="title.length > 0">
        <b-icon-plus></b-icon-plus>
      </b-button>
    </form>
  </div>
</template>

<script>
import uuid from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo: function(event) {
      event.preventDefault();

      if (this.title.length > 0) {
        const newTodo = {
          id: uuid.v4(),
          title: this.title,
          completed: false
        };

        this.$emit("todo-added", newTodo);
        this.title = "";
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
