
<script setup>
  import { defineProps, defineEmits, ref, watchEffect} from 'vue';

  // Define props and emits
  const { job, modalActive } = defineProps(['job', 'modalActive']);
  let localJob = ref(job ? { ...job } : { title: '', icon: '' }); // створіть локальну копію для редагування
const emit = defineEmits(['update', 'delete', 'close', 'toggleFavorite']);

  const close = () => {
    emit('close');
  };

  const saveJobCard = () => {
    // Перевіряємо, чи має localJob ідентифікатор
    if (localJob.value && localJob.value.id) {
      // Якщо ідентифікатор існує, оновлюємо існуючу роботу
      emit('update', localJob.value);
    } else {
      // Ідентифікатора немає, створюємо нову роботу
      emit('create', localJob.value);

    }
    // Закриваємо модальне вікно після збереження
    modalActive.value = false;

  };

  const deleteJobCard = () => {
    emit('delete', localJob.value.id);
    console.log('Form submitted2');
  };
  const toggleFavorite = (job) => {
    emit('toggleFavorite', job);
  };
  watchEffect(() => {
    localJob.value = job ? { ...job } : { title: '', icon: '' };
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
  Height: 356px;
  margin: 100px auto 10px;
  background-color: $color-form-bg;
  border-radius: 30px;
  color: $color-form-text;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin: auto;

}

.card_name_input,
.card_icon_input {
  background-color: $color-form-input;
  border-radius: 10px;
  border: none;
  height: 44px;
  width: 240px;
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
  width: 240px;
  margin: 15px auto 0 auto;
}

.form-link {
  font-size: $font-size-xs;
  color: $color-icons-UI;
}

.form-buttons {
  margin: 20px 0 20px 30px;
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
  position: fixed;
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
                Use the web codes found on Google’s material icons and paste in the box above!
                <a class="form-link" href="https://fonts.google.com/icons" target="_blank">https://fonts.google.com/icons</a>
              </p>
            </div>
<!--            <div class="choose-title-color">Choose a color for the icon:</div>-->
<!--            <input type="color" v-model="localJob.iconColor" @input="updateIconColor">-->
            <div class="form-buttons">
              <button class="btn btn-save" @click.stop="saveJobCard">Save</button>
              <button class="btn btn-cancel" @click="close" type="button">Cancel</button>
              <button class="btn btn-delete" @click.stop="deleteJobCard">Delete</button>
            </div>
          </form>
        </div>
      </transition>
    </div>
  </transition>
</template>



