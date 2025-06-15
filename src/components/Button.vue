<script setup lang="ts">
const props = defineProps<{
  className?: string
  text: string
  id?: string
}>()

const handleClick = (e: MouseEvent) => {
  e.preventDefault()

  const target = document.getElementById('counter')

  if (target && props.id) {
    const offset = window.innerHeight * 0.15;
    const top = target.getBoundingClientRect().top + window.scrollY - offset

    window.scrollTo({ top, behavior: 'smooth' })
  }
}
</script>

<template>
  <a
      :class="`${props.className ?? ''} cta-wrapper`"
      @click="handleClick"
  >
    <div class="cta-button group">
      <div class="bg-circle"/>
      <p class="text">{{ props.text }}</p>
      <div class="arrow-wrapper">
        <img src="/images/arrow-down.svg" alt="arrow"/>
      </div>
    </div>
  </a>
</template>
