<script setup>
import JobCardList from "../components/JobCardList.vue"
</script>

<template>
  <div class="home-wrap">
    <h1 class="home-title">Welcome to Unicorn Jobs, where we display new job roles that combine 2 different careers into
      one.</h1>
  </div>
  <JobCardList></JobCardList>
</template>

<style lang="scss">

@import '../assets/_varibles.scss';

.home-wrap {
  margin: 20px 10px 0 10px;
}

.home-wrap {
  margin: 0 auto;
  text-align: center;
  max-width: 1014px;
}

.home-title {
  max-width: 320px;
  text-align: center;
  margin: 100px auto 10px auto;
  font-size: $font-size-sm;
  text-align: center;
  font-weight: $font-weight-base;
  color: $color-text;
}
</style>