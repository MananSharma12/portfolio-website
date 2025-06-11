<script setup lang="ts">
defineProps<{
  imgPath: string
  name?: string
}>()
</script>

<template>
  <div class="flex-none flex-center marquee-item">
    <img :src="imgPath" :alt="name" />
  </div>
</template>

