<script setup>
import { ref } from "vue";

const openModal = ref(false);

const toggleOpen = () => {
  openModal.value = !openModal.value;
};
</script>

<template>
  <div :class="`min-h-scr1een relative ${openModal && 'overflow-y-hidden'}`">
    <MainHead @openModal="toggleOpen" />
    <NuxtPage />
    <MainFoot />
    <div
      :class="['modal flex justify-between ', { open: openModal }]"
      class="modal"
    >
      <div class="flex-grow " @click="toggleOpen"></div>
      <MainModal @close="toggleOpen" />
    </div>
  </div>
</template>

<style scoped>
.min-h-screen {
  min-height: 100vh;
}
</style>
