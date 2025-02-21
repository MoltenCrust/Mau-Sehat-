<template>
    <div class="app">
      <Navbar />
      <main class="content">
        <router-view></router-view>
      </main>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import Navbar from './components/Navbar.vue';
  
  export default defineComponent({
    name: 'App',
    components: {
      Navbar,
    },
  });
  </script>
  
  <style>
  body {
    margin: 0;
    font-family: Arial, sans-serif;
  }
  .content {
    justify-items: center;
    padding-top: 1rem;
  }
  </style>