<template>
  <div class="todo-item">
    <span
      class="todo-text"
      :class="{ completed: todo.completed }"
    >
      {{ todo.text }}
    </span>
    <div class="todo-actions">
      <button @click="$emit('toggle-complete', todo.id)">Сделано</button>
      <button @click="handleEdit">Редактировать</button>
      <button @click="$emit('delete-todo', todo.id)">Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true,
      properties: {
        id: Number,
        text: String,
        completed: Boolean
      }
    }
  },
  methods: {
    handleEdit() {
      const newText = prompt("Введите новое дело:", this.todo.text);
      if (newText && newText.trim()) {
        this.$emit("edit-todo", {
          id: this.todo.id,
          newText: newText.trim()
        });
      }
    }
  }
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px;
  border: 1px solid #eee;
  margin: 4px 0;
}
.todo-text.completed {
  text-decoration: line-through;
  color: #999;
}
.todo-actions {
  display: flex;
  gap: 8px;
}
button {
  padding: 4px 8px;
  cursor: pointer;
}
</style>