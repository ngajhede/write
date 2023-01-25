<template>
  <span>
    {{ currentTime.toLocaleTimeString("en-US", { hour12: false }) }}
  </span>
</template>
<script setup lang="ts">
import { useCurrentTime } from "../composables/useCurrentTime";

const { currentTime } = useCurrentTime();
</script>
