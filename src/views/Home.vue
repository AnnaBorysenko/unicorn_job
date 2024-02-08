<script setup>
import JobCardList from "../components/JobCardList.vue"
</script>

<template>
  <div class="home-wrap">
  <h1 class="home-title">Welcome to Unicorn Jobs, where we display new job roles that combine 2 different careers into one.</h1>
  </div>
  <JobCardList></JobCardList>
</template>

<style lang="scss">

@import '../assets/_varibles.scss';
.home-wrap {
  margin: 20px 10px 0 10px ;

}
.home-title {
  font-size: $font-size-md;
  color: $color-text;
  text-align: center;
  font-weight: $font-weight-base;
  margin: 100px 0 10px;

}
</style>