<script setup>
import TodoList from "./components/TodoList.vue";
import ObjectOfArray from "./components/ObjectOfArray.vue";
import manual from "./components/manual.vue";
</script>

<template>
  <div></div>
  <TodoList />
  <!-- <manual /> -->
  <ObjectOfArray />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
