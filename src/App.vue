<template>
  <v-app class="app-shell">
    <v-main class="app-main">
      <Home />
    </v-main>
  </v-app>
</template>

<script setup>
import Home from './pages/Home.vue'
</script>

<style>
.app-shell,
.app-main {
  background: var(--bg-body) !important;
  background-color: var(--bg-900) !important;
}
</style>
