<template>
  <section class="todo">
    <input
      type="text"
      class="add-todo"
      autofocus="autofocus"
      placeholder="接下来要做什么？"
      @keyup.enter="addTodo"
    >
    <Items
      v-for="(todo,index) in filteredTodos"
      :key="index"
      :todo="todo"
      @del="deleteTodo(todo.id)"
    />
    <Tabs
      :filter="filter"
      :todos="todos"
      @toggleFilter="toggleFilter"
      @clearCompleted="clearCompleted"
    />
  </section>
</template>

<script>
import Items from "./Items.vue";
import Tabs from "./Tabs.vue";
let id = 0;
export default {
  components: {
    Items,
    Tabs
  },
  data() {
    return {
      todos: [{ id: 1, content: "吃饭", completed: true }],
      filter: "all"
    };
  },
  methods: {
    addTodo(e) {
      this.todos.unshift({
        id: id++,
        content: e.target.value.trim(),
        completed: false
      });
      e.target.value = null;
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1);
    },
    toggleFilter(state) {
      this.filter = state;
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      let isCompleted = this.filter === "completed";
      return this.todos.filter(todo => isCompleted === todo.completed);
    }
  }
};
</script>

<style lang="scss" scoped>
.todo {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px #666;
  .add-todo {
    display: inline-block;
    width: 100%;
    font-size: 24px;
    padding: 6px;
    border: none;
    border-bottom: 1px solid black;
  }
}
</style>
