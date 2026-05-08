<template>
  <div style="margin-top:20px; border:1px solid #ccc; padding:15px;">
    <button @click="handleClick">提交员工信息</button>
  </div>
</template>

<script>
export default {
  name: "EmployeeCard",
  props: {
    func: {
      type: Function,
      required: true
    }
  },
  methods: {
    handleClick() {
      this.func("Иван", 50000)
    }
  }
}
</script>