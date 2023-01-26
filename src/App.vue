import Clock from './components/clock.vue';

<template>
  <Transition as="div" appear appear-active-class="fade-enter-active">
    <main class="max-w-screen-sm min-h-screen mx-auto flex flex-col">
      <header class="flex items-center justify-between px-6 pt-4">
        <h1 class="font-serif italic font-medium">Write</h1>
        <Transition name="fade">
          <span v-if="saveError">
            {{ saveError }}
          </span>
        </Transition>
        <DigitalClock />
      </header>
      <RouterView />
    </main>
  </Transition>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";
import DigitalClock from "./components/DigitalClock.vue";

let saveError = ref<string | null>(null);

const saveErrorMessages = [
  "No need to save...",
  "Your notes are automatically saved",
  "Your note is already saved",
];

onMounted(() => {
  //intercept CTRL S keyboard presses
  document.addEventListener("keydown", (e) => {
    if (e.ctrlKey && e.key === "s") {
      e.preventDefault();
      // show a random message
      const randomIndex = Math.floor(Math.random() * saveErrorMessages.length);
      saveError.value = saveErrorMessages[randomIndex];

      setTimeout(() => {
        saveError.value = null;
      }, 3000);
    }
  });
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;1,6..72,400;1,6..72,500&display=swap");

.fade-enter-active {
  animation: init 1.5s ease-out forwards;
}

@keyframes init {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 3s ease-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
