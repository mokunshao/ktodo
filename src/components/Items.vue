<template>
  <div :class="['todoItem',todo.completed?'completed':'']">
    <label>
      <input type="checkbox" class="toggle" v-model="todo.completed">
      <span>{{todo.content}}</span>
    </label>
    <button class="delete" @click="deleteTodo">x</button>
  </div>
</template>

<script>
export default {
  props: {
    todo: { type: Object, required: true }
  },
  methods: {
    deleteTodo() {
      this.$emit("del", this.todo.id);
    }
  }
};
</script>

<style lang="scss" scoped>
.todoItem {
  background: white;
  width: 100%;
  padding: 6px;
  position: relative;
  input:checked + span {
    text-decoration: line-through;
    color: #999;
  }
  .delete {
    position: absolute;
    right: 5px;
  }
}
</style>
