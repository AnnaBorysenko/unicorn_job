<script setup>
import {provide, reactive} from 'vue';
import Nav from "../src/components/JobNav.vue"
import Home from "../src/views/Home.vue"

//     By choosing the Composition API for this task,
//     I focused on the principles of reactive programming that allow you to effectively manage the state of components.
//     The Composition API allows you to create compact and understandable code,
//     which makes it easier to develop and maintain.
//     In addition, using the Composition API provides more flexibility and control over the structure of components,
//     making development easier and more efficient.

const data = reactive({
  jobs: [
    {id: 1, title: 'Police Pizza Delivery Driver position', icon: 'local_pizza', color: '#72FF5B', isFavorite: false},
    {id: 2, title: 'Frontend Vue.js Developer', icon: 'keyboard', color: '#72FF5B', isFavorite: true},
    {id: 3, title: 'Unicorn Job Name', icon: 'pool', color: '#72FF5B', isFavorite: false},
    {id: 4, title: 'Baker', icon: 'cookie', color: '#72FF5B', isFavorite: true},
    {id: 5, title: 'Unicorn Job Name', icon: 'pool', color: '#72FF5B', isFavorite: false},
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
