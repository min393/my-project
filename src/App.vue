<template>
  <div class="app-container">
    <NotesSidebar
      :notes="notes"
      :selected-id="selectedNoteId"
      @select="selectNote"
      @delete="deleteNote"
      @new="newNote"
    />

    <NotesEditor
      :value="currentNote"
      @save="saveNote"
    />
  </div>
</template>

<script>
import NotesSidebar from './components/NotesSidebar.vue'
import NotesEditor from './components/NotesEditor.vue'

export default {
  name: 'App',
  components: {
    NotesSidebar,
    NotesEditor
  },
  data() {
    return {
      notes: [],
      selectedNoteId: null,
      currentNote: { title: '', content: '' }
    }
  },
  mounted() {
    const data = localStorage.getItem('notes')
    if (data) this.notes = JSON.parse(data)
  },
  methods: {
    selectNote(note) {
      this.selectedNoteId = note.id
      this.currentNote = { ...note }
    },
    newNote() {
      this.selectedNoteId = null
      this.currentNote = { title: '', content: '' }
    },
    saveNote(note) {
      if (!note.title.trim() && !note.content.trim()) {
        alert('不能保存空白笔记')
        return
      }

      if (this.selectedNoteId) {
        const index = this.notes.findIndex(n => n.id === this.selectedNoteId)
        if (index !== -1) {
          this.notes[index] = { ...note, id: this.selectedNoteId }
        }
      } else {
        const newNote = { id: Date.now(), ...note }
        this.notes.push(newNote)
        this.selectedNoteId = newNote.id
      }

      localStorage.setItem('notes', JSON.stringify(this.notes))
      alert('保存成功！')
    },
    deleteNote(id) {
      if (confirm('确定删除？')) {
        this.notes = this.notes.filter(n => n.id !== id)
        localStorage.setItem('notes', JSON.stringify(this.notes))
        if (this.selectedNoteId === id) this.newNote()
      }
    }
  }
}
</script>

<style scoped>
.app-container {
  display: flex;
  max-width: 900px;
  margin: 30px auto;
  height: 550px;
  border: 1px solid #ccc;
  font-family: "Microsoft YaHei", sans-serif;
}
</style>