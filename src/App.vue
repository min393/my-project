<template>
  <div id="app">
    <h1>Чеклист запланированных дел</h1>
    <TodoInput @add-todo="addTodo" />
    <TodoList
      :todos="todos"
      @toggle-complete="toggleComplete"
      @edit-todo="editTodo"
      @delete-todo="deleteTodo"
    />
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: { TodoInput, TodoList },
  data() {
    return {
      // 初始数据，和你示例里的一样
      todos: [
        { id: 1, text: "купить хлеб", completed: false },
        { id: 2, text: "убрать дом", completed: false }
      ]
    };
  },
  methods: {
    addTodo(text) {
      this.todos.push({
        id: Date.now(),
        text,
        completed: false
      });
    },
    toggleComplete(id) {
      const todo = this.todos.find(t => t.id === id);
      if (todo) todo.completed = !todo.completed;
    },
    editTodo({ id, newText }) {
      const todo = this.todos.find(t => t.id === id);
      if (todo) todo.text = newText;
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 600px;
  margin: 20px auto;
  padding: 0 16px;
}
</style>