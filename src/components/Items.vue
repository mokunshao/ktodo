<template>
  <div :class="['todoItem',todo.completed?'completed':'']">
    <label class="checkbox">
      <input class="checkbox" type="checkbox" v-model="todo.completed">
      <span>{{todo.content}}</span>
    </label>
    <a class="delete" @click="deleteTodo"></a>
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
  font-size: 20px;
  padding: 10px;
  position: relative;
  input + span {
    padding-left: 10px;
  }
  input:checked + span {
    text-decoration: line-through;
    color: #999;
    padding-left: 10px;
  }
  .delete {
    position: absolute;
    right: 5px;
  }
}
</style>
