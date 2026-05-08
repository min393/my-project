<template>
  <div class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-complete="$emit('toggle-complete', $event)"
      @edit-todo="$emit('edit-todo', $event)"
      @delete-todo="$emit('delete-todo', $event)"
    />
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
.todo-list {
  margin-top: 16px;
}
</style>
