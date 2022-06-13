<template>
  <nav>
    <router-link to="/">Projects</router-link>
    <router-link to="/add">Add new project</router-link>
  </nav>
</template>

<script setup lang="ts"></script>

<style scoped>
nav {
  @apply w-full p-3 my-6;
}

nav a {
  @apply px-3 py-2 text-gray-700 hover:bg-gray-100 mx-2;
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  @apply border-b-2 border-green-400;
}
</style>
