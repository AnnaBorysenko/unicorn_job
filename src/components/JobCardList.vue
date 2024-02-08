<script setup>
import { inject, ref } from 'vue';
import JobCard from '../components/JobCard.vue';
import JobModel from "../components/JobModel.vue";

const jobsData = inject('jobsData');
const modalActive = ref(false);

const toggleModal = () => {
  modalActive.value = !modalActive.value;
};

// Logic for adding a new job to jobsData or another state where you store jobs
const createJob = (newJob) => {
  jobsData.jobs.push({...newJob, id: Date.now()});
};

</script>

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

<style lang="scss">
@import '../assets/_varibles.scss';

.icon-add-container {
  width: 96px;
  height: 95px;
  background-color: $color-icons-UI;
  color: $color-icon-wrap;
  font-size: 48px;
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
