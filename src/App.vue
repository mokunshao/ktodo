<template>
  <div id="app">
    <div id="cover"></div>
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
#app {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  #cover {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: #999;
    opacity: 0.3;
    z-index: -1;
  }
}
</style>
