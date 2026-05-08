<template>
  <div class="form-card">
    <input v-model="newName" placeholder="Имя">
    <input v-model="newSurn" placeholder="Фамилия">
    
    <div class="form-buttons">
      <button @click="save">Сохранить（保存）</button>
      <button @click="$emit('close')">Отмена（取消）</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newName: '',
      newSurn: ''
    }
  },
  methods: {
    save() {
      this.$emit('save', {
        name: this.newName,
        surname: this.newSurn
      })
      this.newName = ''
      this.newSurn = ''
    }
  }
}
</script>

<style scoped>
.form-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  gap: 12px;
  width: 300px;
}

.form-buttons {
  display: flex;
  gap: 8px;
  justify-content: flex-end;
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