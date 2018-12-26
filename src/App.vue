<template>
  <div id="app">
    <Header/>
    <Todo/>
    <Footer/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Todo from "./components/Todo.vue"
import Footer from "./components/Footer.jsx";

export default {
  name: "app",
  components: {
    Header,
    Todo,
    Footer
  }
};
</script>

<style lang="scss">
</style>
