<template>
  <div class="sidebar">
    <input
      type="text"
      class="search-input"
      placeholder="搜索笔记..."
      v-model="searchQuery"
    >

    <div class="notes-list">
      <div
        class="note-item"
        :class="{ active: selectedId === note.id }"
        v-for="note in filteredNotes"
        :key="note.id"
        @click="$emit('select', note)"
      >
        <span>{{ note.title || "无标题笔记" }}</span>
        <button class="delete-btn" @click.stop="$emit('delete', note.id)">×</button>
      </div>
    </div>

    <button class="new-btn" @click="$emit('new')">+ 新建笔记</button>
  </div>
</template>

<script>
export default {
  name: 'NotesSidebar',
  props: {
    notes: {
      type: Array,
      default: () => []
    },
    selectedId: {
      type: Number,
      default: null
    }
  },
  data() {
    return {
      searchQuery: ''
    }
  },
  computed: {
    filteredNotes() {
      if (!this.searchQuery.trim()) return this.notes
      const q = this.searchQuery.toLowerCase()
      return this.notes.filter(n =>
        n.title.toLowerCase().includes(q) || n.content.toLowerCase().includes(q)
      )
    }
  }
}
</script>

<style scoped>
.sidebar {
  width: 260px;
  border-right: 1px solid #ccc;
  padding: 12px;
  display: flex;
  flex-direction: column;
  background: #f9f9f9;
}
.search-input {
  padding: 6px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.notes-list {
  flex: 1;
  overflow-y: auto;
  margin-bottom: 10px;
}
.note-item {
  padding: 8px;
  cursor: pointer;
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
}
.note-item.active {
  background: #e0e0e0;
}
.delete-btn {
  border: none;
  background: none;
  color: red;
  cursor: pointer;
}
.new-btn {
  padding: 6px;
  cursor: pointer;
}
</style>