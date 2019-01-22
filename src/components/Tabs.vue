<template>
  <div class="helper">
    <div>还有{{unfinishiedLength}}个任务未完成</div>
    <div
      class="button"
      v-for="state in states"
      :key="state.en"
      :class="[state.en,filter === state.en?'':'is-outlined',state.en==='completed'?'is-success':'is-info']"
      @click="toggleFilter(state.en)"
    >{{state.cn}}</div>
    <div class="button is-danger is-outlined" @click="clearCompleted">清除已完成</div>
  </div>
</template>

<script>
export default {
  props: {
    filter: {
      type: String,
      required: true
    },
    todos: {
      type: Array,
      required: true
    }
  },
  computed: {
    unfinishiedLength() {
      return this.todos.filter(todo => !todo.completed).length;
    }
  },
  data() {
    return {
      states: [
        { en: "all", cn: "所有" },
        { en: "active", cn: "未完成" },
        { en: "completed", cn: "已完成" }
      ]
    };
  },
  methods: {
    clearCompleted() {
      this.$emit("clearCompleted");
    },
    toggleFilter(state) {
      this.$emit("toggleFilter", state);
    }
  }
};
</script>

<style lang="scss" scoped>
.helper {
  & > * {
    margin: 10px;
  }
}
</style>

