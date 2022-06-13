<template>
  <Navigation />
  <router-view />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Navigation from "./components/NavigationItem.vue";

export default defineComponent({
  components: {
    Navigation,
  },
});
</script>

<style>
#app {
  @apply m-auto flex flex-col items-center bg-gray-100 w-screen h-screen;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
