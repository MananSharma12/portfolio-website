<script setup lang="ts">
const props = defineProps<{
  className?: string
  text: string
  id?: string
}>()
</script>

<template>
  <a :class="`${props.className ?? ''} cta-wrapper`">
    <div class="cta-button group">
      <div class="bg-circle"/>
      <p class="text">{{ props.text }}</p>
      <div class="arrow-wrapper">
        <img src="/images/arrow-down.svg" alt="arrow"/>
      </div>
    </div>
  </a>
</template>

<style scoped>

</style>