<script setup>
import {defineProps, defineEmits, ref, inject} from 'vue';
import JobModal from "../components/JobModal.vue";

defineProps({
  job: Object
})

const modalActive = ref(false);
const jobsData = inject('jobsData');
const emit = defineEmits(['update-favorite'])

const toggleFavorite = (job) => {
  job.isFavorite = !job.isFavorite;
// Emit an update event to save the state change in the general state of the application
  emit('update-favorite', job);
};

//  This function is designed to update the job object in the array of jobs stored in the jobsData object,
//  replacing the old object with a new one using the job ID.
const updateJob = (updatedJob) => {
  const index = jobsData.jobs.findIndex(job => job.id === updatedJob.id);
  if (index !== -1) {
    jobsData.jobs[index] = updatedJob;
  }
};
const deleteJob = (jobId) => {
  if (jobsData && jobsData.jobs) {
    const index = jobsData.jobs.findIndex(job => job.id === jobId);
    if (index !== -1) {
      jobsData.jobs.splice(index, 1);
    }
  } else {
    console.error('jobsData is not defined or does not contain jobs');
  }
};
const toggleModal = () => {
  modalActive.value = !modalActive.value;
};
</script>

<template>
  <div class="job-card-wrap">
    <div class="job-card">
      <div class="icon-edit-container">
        <span @click="toggleModal" class="material-icons">edit</span>
      </div>
      <JobModal
          @update="updateJob"
          @delete="deleteJob"
          @close="toggleModal"
          :modalActive="modalActive"
          :job="job"
      />

      <div class="icon-chosen-container">
        <span class="material-icons"
              :style="{'color': job.color}"
        >{{ job.icon }}</span>
      </div>

      <div class="icon-favorite-container">
        <span
            class="material-icons"
            :class="{ 'favorite': job.isFavorite }"
            @click="toggleFavorite(job)"
        >
          {{ job.isFavorite ? 'favorite' : 'favorite_border' }}
        </span>
      </div>
    </div>
    <div class="job-card-title">{{ job.title }}</div>
  </div>
</template>

<style lang="scss">
@import '../assets/_varibles.scss';

.job-card-wrap {
  max-width: 304px;
  width: 304px;
  height: 356px;
  flex-basis: 33.333333%;
  background-color: $color-bg;
  margin: 30px auto;
  border-radius: 30px;
  padding-top: 30px;
  border: 1px solid $color-bg;
  transition: transform 0.3s ease;
}

.job-card-wrap:hover {
  border: 1px solid $color-icons-UI;
  transform: translateY(-10px);

  .icon-edit-container .material-icons {
    background-color: $color-icons-UI;
    color: $color-bg;
  }
}

.job-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 248px;
  height: 248px;
  margin: 0 30px;
  background-color: $color-icon-wrap;
  border-radius: 20px;
}

.job-card > *:first-child {
  align-self: flex-end;
}

.job-card .icon-chosen-container {
  align-self: center;
}

.job-card .icon-favorite-container {
  align-self: flex-start;
}

.icon-edit-container .material-icons {
  width: 60px;
  height: 60px;
  background-color: $color-icon-wrap;
  color: $color-icon-wrap;
  font-size: 24px;
  border-radius: 50%;
  padding: 18px;
  margin: 10px 10px 0 0;
}

.icon-favorite-container .material-icons {
  font-size: 24px;
  color: $color-icons-UI;
  margin: 0 0 10px 10px;

}

.icon-favorite-container .material-icons.favorite {
  color:$color-icon-favorite;
}

.icon-chosen-container .material-icons {
  font-size: 96px;
}

.job-card-title {
  padding: 10px 0 0 45px;
  font-size: $font-size-sm;
  font-wight: $font-weight-base;
  color: $color-text;
}
</style>
