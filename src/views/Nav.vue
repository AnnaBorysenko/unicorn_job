<script setup>
import {ref, inject, watchEffect} from 'vue';

// Is used to retrieve values that were provided at a higher level in the component tree.
const jobsData = inject('jobsData');

const favoriteCount = ref(0);

//  Is used to automatically track changes in the jobsData.jobs list and update the favoriteCount.value.
//  It filters the list of jobs to find only those that are labeled "favorite"
watchEffect(() => {
  if (jobsData && jobsData.jobs) {
    favoriteCount.value = jobsData.jobs.filter(job => job.isFavorite).length;
  }
});
</script>

<template>
  <div class="nav-wrap">
    <div class="nav">
      <div class="nav-logo">
        <div class="nav-logo-text">Unicorn Jobs -
          <span class="favorite-count">{{ favoriteCount }}</span>
          <span class="favorite-text">Saved</span>
        </div>
      </div>
      <div class="nav-burger-menu">
        <span class="material-icons">menu</span>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import '../assets/_varibles.scss';

.nav-wrap {
  position: fixed;
  z-index: 999;
  width: 100%;
  top: 0;
  background-color: $color_bg;
}

.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 80px;
  margin: 0 10px;
  color: $color-text;
  font-weight: $font-weight-base;
}

.favorite-count {
  position: absolute;
  color: $color-icons-UI;
  left: 128px;

}
.favorite-text {
  margin: 14px;
}

.nav-logo-text {
  font-size: $font-size-sm;
}

.nav-burger_menu .material-icons {
  color: $color-icons-UI;
  font-size: 48px;
}
</style>
