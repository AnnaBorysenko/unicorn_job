<script setup>
import { ref, inject, watchEffect } from 'vue';

// Assuming 'jobsData' is provided by a parent component or a plugin
const jobsData = inject('jobsData');

const favoriteCount = ref(0);

// Automatically update favoriteCount whenever jobsData.jobs changes
watchEffect(() => {
  if (jobsData && jobsData.jobs) {
    favoriteCount.value = jobsData.jobs.filter(job => job.isFavorite).length;
  }
});
</script>

<template>
  <div class="nav_wrap">
    <div class="nav">
      <div class="nav_logo">
        <div class="nav_logo_text">Unicorn Jobs - {{ favoriteCount }} Saved</div>
      </div>
      <div class="nav_burger_menu">
        <span class="material-icons">menu</span>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import '../assets/_varibles.scss';

.nav_wrap {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 999;
  background-color: $color_bg;
}

.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 0 10px;
  color: $color-text;
  height: 80px;
  font-weight: $font-weight-base;
}

.nav_logo_text {
  font-size: $font-size-sm;
}

.nav_burger_menu .material-icons {
  color: $color-icons-UI;
  font-size: 48px;
}
</style>
