<script setup>
import { provide, reactive } from 'vue';
// чому Composition API
import Nav from "../src/views/Nav.vue"
import Home from "../src/views/Home.vue"


const data = reactive({
  jobs: [
    { id: 1, title: 'Police Pizza Delivery Driver position', icon: 'local_pizza', isFavorite: false },
    { id: 2, title: 'Frontend Vue.js Developer', icon: 'keyboard', isFavorite: false },
    { id: 3, title: 'Unicorn Job Name', icon: 'pool', isFavorite: false },
    { id: 4, title: 'Baker', icon: 'cookie', isFavorite: false },
    { id: 5, title: 'Unicorn Job Name', icon: 'pool', isFavorite: false },
  ]
});

provide('jobsData', data);

</script>

<template>
  <Nav></Nav>
  <Home></Home>
</template>

<style lang="scss">
@import './assets/_varibles.scss';

body {
  background: $color_main_bg;
  margin: 0;
}

</style>
