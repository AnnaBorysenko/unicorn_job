<script setup>
import {defineProps, defineEmits, ref, watchEffect} from 'vue';

// Define props and emits
const {job, modalActive} = defineProps(['job', 'modalActive']);
let localJob = ref(job ? {...job} : {title: '', icon: ''});
const emit = defineEmits(['update', 'delete', 'close', 'toggleFavorite']);

const saveJobCard = () => {
  if (localJob.value && localJob.value.id) {
    emit('update', localJob.value);
  } else {
    emit('create', localJob.value);
  }
  emit('close');
};

const deleteJobCard = () => {
  emit('delete', localJob.value.id);
};
const toggleFavorite = (job) => {
  emit('toggleFavorite', job);
};

const close = () => {
  emit('close');
};
watchEffect(() => {
  localJob.value = job ? {...job} : {title: '', icon: ''};
});

</script>

<style lang="scss">
@import '../assets/_varibles.scss';

.icon-exit-container {
  background-color: $color-icons-UI;
  height: 56px;
  width: 56px;
  border-radius: 50%;
  position: absolute;
  top: -20px;
  right: -20px;
  color: $color-bg;
}

.icon-exit-container .material-icons {
  margin: 15px 0 0 15px;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  Width: 304px;
  Height: 400px;
  padding-top: 10px;
  margin: 100px auto 10px;
  background-color: $color-form-bg;
  border-radius: 30px;
  color: $color-form-text;
}

.main-form-wrap {
  max-width: 240px;
  margin: auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin: auto;
  width: 240px;
  padding-bottom: 15px;
}

.card_name_input,
.card_icon_input {
  background-color: $color-form-input;
  border-radius: 10px;
  border: none;
  height: 44px;
  color: $color-form-text;
  padding-left: 10px;

}

.card_name_input:not([type=file]),
.card_icon_input:not([type=file]) {
  outline: none;
}

.input-instruction {
  color: $color-form-text;
  font-size: $font-size-xs;
  margin: 15px auto 0 auto;
}

.input-instruction-icon {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

.form-link {
  font-size: $font-size-xs;
  color: $color-icons-UI;
}

.form-buttons {
  display: flex;
  justify-content: space-around;
}

.btn-container {
  display: flex;
}

.btn {
  width: 60px;
  height: 30px;
  border-radius: 19px;
  border: none;
}

.btn-save {
  background-color: $color-icons-UI;
  margin-right: 10px;
}

.btn-cancel {
  background-color: $color-form-btn-cancel;
  margin-right: 60px;
  color: $color-icons-UI;
}

.btn-delete {
  background-color: $color-form-btn-delete;

}

.modal-mask {
  position: absolute;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
}

.modal-container {
  margin: 150px auto;
  padding: 20px 30px;
  border-radius: 2px;
}

.modal-animation-enter-active,
.modal-animation-leave-active {
  transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-animation-enter-from,
.modal-animation-leave-to {
  opacity: 0;
}

.modal-animation-inner-enter-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}

.modal-animation-inner-leave-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-animation-inner-enter-from {
  opacity: 0;
  transform: scale(0.8);
}

.modal-animation-inner-leave-to {
  transform: scale(0.8);
}

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  position: fixed;
  top: 0;
  left: 0;
  background-color: $color-main_bg;

  .modal-inner {
    position: relative;
    padding: 64px 16px;
  }
}

input[type="color" i] {
  margin-top: 10px;
  border: 3px;
  inline-size: 60px;
  block-size: 60px;

}

</style>

<template>
  <transition name="modal-animation">
    <div v-show="modalActive" class="modal modal-mask">
      <transition name="modal-animation-inner">
        <div v-show="modalActive" class="modal-inner">
          <form class="form" @submit.prevent="saveJobCard">
            <div @click="close" class="icon-exit-container">
              <span class="material-icons">close</span>
            </div>
            <div class="main-form-wrap">
              <div class="input-wrap">
                <div class="input-container">
                  <label for="card-name" class="card-name-label">Name of Unicorn Job</label>
                  <input
                      placeholder="Enter job title"
                      v-model="localJob.title"
                      type="text"
                      id="card_name"
                      class="card_name_input"
                  >
                </div>
                <div class="input-container">
                  <label for="card-icon" class="card-icon-label">Material Icon</label>
                  <input
                      placeholder="Enter job icon"
                      v-model="localJob.icon"
                      type="text"
                      id="card-icon"
                      class="card_icon_input"
                  >
                  <p class="input-instruction">
                    <div class="input-instruction-icon">
                      Use the web codes found on Google’s material icons and paste in the box above!
                      <a class="form-link" href="https://fonts.google.com/icons" target="_blank">https://fonts.google.com/icons</a>
                    </div>
                    <div class="input-instruction-color">
                      <div class="choose-title-color">Choose a color for the icon:</div>
                      <input class="choose-color" type="color">
                    </div>
                  </p>
                </div>
              </div>
              <div class="form-buttons">
                <div class="btn-container">
                  <button class="btn btn-save" @click.stop="saveJobCard">Save</button>
                  <button class="btn btn-cancel" @click="close" type="button">Cancel</button>
                </div>
                <button class="btn btn-delete" @click.stop="deleteJobCard">Delete</button>
              </div>
            </div>
          </form>
        </div>
      </transition>
    </div>
  </transition>
</template>



