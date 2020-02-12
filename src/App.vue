<template>
  <div id="app">
    <div class="container">
      <TodosList />
    </div>
  </div>
</template>

<script>
import TodosList from "./components/todosList";
export default {
  name: "App",
  components: {
    TodosList
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  background-color: #f4f4f4;
  background-repeat: no-repeat;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0e1a5d;
  min-height: 100vh;
}
.container {
  max-width: 800px;
  margin: 0 auto;
}
@media only screen and (max-width: 420px) {
  .container {
    padding: 0 15px
  }
}
</style>
