<template>
  <div id="app">
    <TodoApp v-bind:tasks="tasks" />
  </div>
</template>

<script>
import TodoApp from "./components/TodoApp";
export default {
  name: "App",
  components: {
    TodoApp,
  },
};
</script>

<style></style>
