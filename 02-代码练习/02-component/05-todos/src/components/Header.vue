<template>
  <div class="todo-header">
    <input
      @keyup.enter="handleEnter"
      v-model="name"
      type="text"
      placeholder="请输入你的任务名称，按回车键确认"
    />
  </div>
</template>

<script>
export default {
  props: {
    addTodo: Function,
  },
  data() {
    return {
      name: "",
    };
  },
  methods: {
    handleEnter() {
      const name = this.name.trim();
      if (!name) {
        alert("请输入内容~");
        return;
      }
      this.addTodo(name);
      this.name = "";
    },
  },
};
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
