<template>
  <section class="todo">
    <div class="field">
      <div class="control">
        <input
          class="add-todo input is-info is-large is-rounded"
          type="text"
          autofocus="autofocus"
          placeholder="接下来要做什么？"
          @keyup.enter="addTodo"
          v-model="inputValue"
        >
        <a class="addTodo button is-info is-rounded" @click="addTodo">添加</a>
      </div>
    </div>
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
let localTodos = JSON.parse(window.localStorage.getItem("todos")) || [];
let id = localTodos.length || 0;
export default {
  components: {
    Items,
    Tabs
  },
  data() {
    return {
      todos: localTodos,
      filter: "all",
      inputValue: ""
    };
  },
  methods: {
    addTodo() {
      if (this.inputValue) {
        this.todos.unshift({
          id: id++,
          content: this.inputValue.trim(),
          completed: false
        });
        this.inputValue = "";
      }
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
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
.control {
  position: relative;
  margin: 10px;
  .addTodo {
    position: absolute;
    right: 10px;
    top: 10px;
  }
}
</style>
