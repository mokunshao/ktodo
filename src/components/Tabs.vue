<template>
  <div class="helper">
    <span class="left">{{unfinishiedLength}} items left</span>
    <span class="tabs">
      <span
        v-for="state in states"
        :key="state"
        :class="[state,filter === state?'actived':'']"
        @click="toggleFilter(state)"
      >{{state}}</span>
    </span>
    <span class="clear" @click="clearCompleted">Clear completed</span>
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
      states: ["all", "active", "completed"]
    };
  },
  methods: {
    clearCompleted() {
      this.$emit('clearCompleted')
    },
    toggleFilter(state) {
      this.$emit("toggleFilter", state);
    }
  }
};
</script>

<style lang="scss" scoped>
.helper {
  background: white;
  width: 100%;
  padding: 6px;
  text-align: center;
  .left {
    float: left;
  }
  .clear {
    float: right;
  }
  .tabs {
    & > * {
      padding: 0 5px;
      border: transparent solid;
    }
    .actived {
      border: red solid;
      border-radius: 5px;
    }
  }
}
</style>

