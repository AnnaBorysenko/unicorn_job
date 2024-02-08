<template>
  <div class="job-list">
    <JobCard
        v-for="job in jobsData?.jobs"
        :key="job.id"
        :job="job"
    />
    <div class="job-card-wrap">
      <div class="job-card add">
        <div class="icon-add-container">
          <span
              @click="toggleModal"
              class="material-icons">
            add
          </span>
        </div>
      </div>
      <div class="job-card-title add-title">Add new Unicorn</div>
      <JobModel
          @create="createJob"
          @close="toggleModal"
          :modalActive="modalActive"/>
    </div>
  </div>
</template>

<script setup>
import { inject, ref } from 'vue';
import JobCard from '../components/JobCard.vue';
import JobModel from "../components/JobModel.vue";


const jobsData = inject('jobsData');
console.log(jobsData);
const modalActive = ref(false);


const toggleModal = () => {
  modalActive.value = !modalActive.value;
};

// Метод для оновлення робочого місця
const createJob = (newJob) => {
  // Логіка для додавання нової роботи до jobsData або іншого стану, де ви зберігаєте роботи
  jobsData.jobs.push({...newJob, id: Date.now()});
  modalActive.value = false;
};

</script>
<style lang="scss">
@import '../assets/_varibles.scss';

.icon-add-container {
  font-size: 48px;
  Width: 96px;
  Height: 95px;
  background-color: $color-icons-UI;
  color: $color-icon-wrap;
  border-radius: 50%;
  padding: 15px 36px;
  margin: 100px auto;
}

.job-card.add {
  background-color: $color-bg;
}
.job-card-title.add-title {
  padding: 10px 0 0 75px;
}
</style>
