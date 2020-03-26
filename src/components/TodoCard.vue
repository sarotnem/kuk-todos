<template>
  <div class="todo-card" :class="{'completed': todo.completed}">
    <div class="complete-btn">
      <div class="square" @click="toggleTodoComplete" :class="{ 'completed': todo.completed }">
        <b-icon-check class="icon" :class="{ 'completed': todo.completed }"></b-icon-check>
      </div>
    </div>
    <!-- Show this div if in normal mode -->
    <div v-if="!editing">
      <div class="text" :class="{ 'completed': this.todo.completed }">{{todo.title}}</div>
      <div class="edit-btn" @click="editTodo">
        <b-icon-pencil class="icon"></b-icon-pencil>
      </div>
      <div class="destroy-btn" @click="deleteTodo">
        <b-icon-trash class="icon"></b-icon-trash>
      </div>
    </div>
    <!-- Show this div if in edit mode -->
    <div v-if="editing">
      <div class="edit">
        <input type="text" v-model="tempTitle" @keyup.enter="acceptEdit" />
      </div>
      <div class="edit-accept-btn" @click="acceptEdit">
        <b-icon-check class="icon"></b-icon-check>
      </div>
      <div class="edit-cancel-btn" @click="cancelEdit">
        <b-icon-x class="icon"></b-icon-x>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoCard",
  props: ["todo"],
  data() {
    return {
      editing: false,
      tempTitle: ""
    };
  },
  methods: {
    toggleTodoComplete: function() {
      this.todo.completed = !this.todo.completed;
    },
    deleteTodo: function() {
      this.$emit("todo-deleted", this.todo);
    },
    editTodo: function() {
      this.tempTitle = this.todo.title;
      this.editing = true;
    },
    acceptEdit: function() {
      if (this.tempTitle.length > 0) this.todo.title = this.tempTitle;
      this.tempTitle = "";
      this.editing = false;
    },
    cancelEdit: function() {
      this.tempTitle = "";
      this.editing = false;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
