<template>
  <div class="p-14">
    <RouterLink
      class="flex justify-center text-4xl text-yellow-700"
      :to="{ name: 'Home' }"
      >Pokemon Picker</RouterLink
    >
  </div>
  <RouterView />
</template>

<script setup>
import { RouterView, RouterLink } from "vue-router";
</script>

<style>
@import "@/assets/base.css";
</style>
