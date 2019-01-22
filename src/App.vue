<template>
  <div id="app">
    <Header/>
    <Todo/>
  </div>
</template>

<script>
import 'bulma/css/bulma.css'
import Header from "./components/Header.vue";
import Todo from "./components/Todo.vue"

export default {
  name: "app",
  components: {
    Header,
    Todo
  }
};
</script>

<style lang="scss">
</style>
