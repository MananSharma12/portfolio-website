<script setup lang="ts">
const { title, sub } = defineProps<{
  title: string,
  sub: string,
}>()
</script>

<template>
  <div class="flex flex-col items-center gap-5">
    <div class="hero-badge">
      <p>{{ sub }}</p>
    </div>
    <div class="font-semibold md:text-5xl text-3xl text-center">
      {{ title }}
    </div>
  </div>
</template>
