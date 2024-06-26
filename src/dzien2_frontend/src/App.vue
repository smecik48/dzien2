<script setup>
import { ref } from 'vue';
import { dzien2_backend } from 'declarations/dzien2_backend/index';
import Blog from './components/Blog.vue';
let greeting = ref('');

</script>

<template>
  <main class="container mx-auto">
    <img src="/logo2.svg" alt="DFINITY logo" />
    
    <Blog />
  </main>
</template>
