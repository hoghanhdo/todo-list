<template>
  <div></div>
  <todo-app></todo-app>
</template>

<script>
import TodoApp from "./components/TodoApp.vue";

export default {
  name: "App",
  data() {
    return {
      msg: "Hello World",
    };
  },
  components: {
    TodoApp,
  },
};
</script>
