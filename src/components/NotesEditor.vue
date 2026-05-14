<template>
  <div class="editor">
    <input
      type="text"
      class="title-input"
      placeholder="笔记标题"
      v-model="localNote.title"
    >
    <textarea
      class="content-area"
      placeholder="笔记内容"
      v-model="localNote.content"
    ></textarea>
    <button class="save-btn" @click="$emit('save', localNote)">保存笔记</button>
  </div>
</template>

<script>
export default {
  name: 'NotesEditor',
  props: {
    value: {
      type: Object,
      default: () => ({ title: '', content: '' })
    }
  },
  data() {
    return {
      localNote: { ...this.value }
    }
  },
  watch: {
    value: {
      handler(val) {
        this.localNote = { ...val }
      },
      immediate: true
    }
  }
}
</script>

<style scoped>
.editor {
  flex: 1;
  padding: 12px;
  display: flex;
  flex-direction: column;
}
.title-input {
  padding: 6px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.content-area {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: none;
  margin-bottom: 10px;
}
.save-btn {
  padding: 6px;
  cursor: pointer;
}
</style>