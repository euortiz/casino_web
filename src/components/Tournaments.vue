<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import CustomButton from './CustomButton.vue';

const days = ref('00');
const hours = ref('00');
const minutes = ref('00');
const seconds = ref('00');

let intervalId: number;

onMounted(() => {
  const targetDate = new Date();
  targetDate.setDate(targetDate.getDate() + 5); // 5 days from now

  intervalId = setInterval(() => {
    const now = new Date();
    const diff = targetDate.getTime() - now.getTime();

    if (diff <= 0) {
      days.value = '00';
      hours.value = '00';
      minutes.value = '00';
      seconds.value = '00';
      clearInterval(intervalId);
    } else {
      days.value = Math.floor(diff / (1000 * 60 * 60 * 24)).toString().padStart(2, '0');
      hours.value = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)).toString().padStart(2, '0');
      minutes.value = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)).toString().padStart(2, '0');
      seconds.value = Math.floor((diff % (1000 * 60)) / 1000).toString().padStart(2, '0');
    }
  }, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <div class="my-20 lg;px-20 main-container py-20 flexCenter" v-motion-slide-visible-left>
    <div class="flex flex-col gap-2 text-white lg:text-[2rem] text-[1.5rem] lg:ml-[60%] bg-preto/50 p-5">
      <span class="text-[1rem] my-3 opacity-50">TOURNAMENTS</span>
      <strong class="mt-5">DAILY SLOT RACE</strong>
      <strong><span class="text-red-500">721.80 EUR + 1000 FS </span>EVERY DAY!</strong>
      <div class=" flex flex-col gap-2">
        <strong class="text-[1rem] mt-10">TOURNAMENT OVER</strong>
        <div class="flex gap-5 flex-wrap items-center">
          <p>
            <span class="bg-cinza/70 py-1 px-2 rounded-lg">{{ days }}d</span>
            :
            <span class="bg-cinza/70 py-1 px-2 rounded-lg">{{ hours }}h</span>
            :
            <span class="bg-cinza/70 py-1 px-2 rounded-lg">{{ minutes }}m</span>
            :
            <span class="bg-cinza/70 py-1 px-2 rounded-lg">{{ seconds }}s</span>
          </p>
          <CustomButton title="PLAY NOW" bg-color="red" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  background-image: url('../assets/tournaments/bgtour.svg');
  background-size: cover;
  background-position: center;
}

.btn_playnow {
  transition: background-color 0.3s ease;
}

.btn_playnow:hover {
  background-color: rgb(136, 0, 136);
}
</style>