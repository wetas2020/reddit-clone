<script setup>
import { RouterView } from 'vue-router'
import UserPosts from '@/components/UserPosts.vue'
</script>

<template>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="#">/r/rarepuppers</a>
  </nav>
  <UserPosts />
  <RouterView />
</template>

<style scoped></style>
