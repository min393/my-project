<template>
  <div style="border: 1px solid #ccc; padding: 10px; margin: 5px 0;">
    <span>{{ name }} {{ surn }}</span>
    <button @click="$emit('remove', id)">remove</button>
  </div>
</template>

<script>
export default {
  name: 'UserItem', // ✅ 多个单词，符合规范
  props: {
    id: Number,
    name: String,
    surn: String
  }
}
</script>