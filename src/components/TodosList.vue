<template>
  <div class="todos">
    <transition-group name="todos-list" tag="ul" class="todos-list">
      <li v-for="todo in todos" :key="todo.id">
        <TodoCard :todo="todo" @todo-deleted="$emit('todo-deleted', todo)"></TodoCard>
      </li>
      </transition-group>
  </div>
</template>

<script>
import TodoCard from '@/components/TodoCard'

export default {
  name: "TodosList",
  components: {
    TodoCard
  },
  props: ['todos'],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.todos-list-enter-active, .todos-list-leave-active {
  transition: all .4s ease-in-out;
}
.todos-list-enter, .todos-list-leave-to {
  opacity: 0;
  transform: translateX(30%);
}
</style>
