<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { logoIconsList } from "../constants";
import LogoIcon from "../components/LogoIcon.vue";

const marqueeRef = ref<HTMLElement>()
const isVisible = ref(true)

const handleVisibilityChange = () => {
  isVisible.value = !document.hidden
  const marqueeBox = marqueeRef.value?.querySelector('.marquee-box') as HTMLElement
  if (marqueeBox) {
    marqueeBox.style.animationPlayState = isVisible.value ? 'running' : 'paused'
  }
}

const setupIntersectionObserver = () => {
  if (!marqueeRef.value) return

  const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          const marqueeBox = entry.target.querySelector('.marquee-box') as HTMLElement
          if (marqueeBox) {
            marqueeBox.style.animationPlayState = entry.isIntersecting ? 'running' : 'paused'
          }
        })
      },
      { threshold: 0.1 }
  )

  observer.observe(marqueeRef.value)

  return () => observer.disconnect()
}

onMounted(() => {
  document.addEventListener('visibilitychange', handleVisibilityChange)
  const cleanup = setupIntersectionObserver()

  onBeforeUnmount(() => {
    document.removeEventListener('visibilitychange', handleVisibilityChange)
    cleanup?.()
  })
})
</script>

<template>
  <div class="md:my-20 my-10 relative" ref="marqueeRef">
    <div class="gradient-edge" />
    <div class="gradient-edge" />

    <div class="marquee h-52">
      <div class="marquee-box md:gap-12 gap-5">
        <template v-for="n in 2" :key="n">
          <LogoIcon
              v-for="({ imgPath }, index) in logoIconsList"
              :key="`${n}-${index}`"
              :imgPath="imgPath"
          />
        </template>
      </div>
    </div>
  </div>
</template>