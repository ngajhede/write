import Clock from './components/clock.vue';

<template>
  <Transition as="div" appear appear-active-class="fade-enter-active">
    <main class="max-w-screen-sm min-h-screen mx-auto flex flex-col">
      <header class="flex items-center justify-between px-6 pt-4">
        <h1 class="font-serif italic font-medium">Write</h1>
        <DigitalClock />
      </header>
      <RouterView />
    </main>
  </Transition>
</template>

<script lang="ts" setup>
import DigitalClock from "./components/DigitalClock.vue";
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
</style>
