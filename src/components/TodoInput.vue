<template>
  <div class="todo-input">
    <input
      type="text"
      v-model="newTodoText"
      placeholder="Новое дело"
      @keyup.enter="handleAdd"
    >
    <button @click="handleAdd">Добавить</button>
  </div>
</template>

<script>
export default {
  name: "TodoInput",
  data() {
    return {
      newTodoText: ""
    };
  },
  methods: {
    handleAdd() {
      if (this.newTodoText.trim()) {
        // 向父组件发送添加事件
        this.$emit("add-todo", this.newTodoText.trim());
        this.newTodoText = ""; // 清空输入框
      }
    }
  }
};
</script>

<style scoped>
/* 这里先不写复杂样式，和你当前的风格保持一致 */
.todo-input {
  margin: 16px 0;
  display: flex;
  gap: 8px;
}
input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  padding: 6px 12px;
  cursor: pointer;
}
</style>