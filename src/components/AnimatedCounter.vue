<script setup lang="ts">
import { ref, computed, onBeforeUnmount } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { gsap } from 'gsap'
import { counterItems } from '../constants'

const counterRefs = counterItems.map(() => ref(0))
const counterContainer = ref<HTMLElement>()
const hasAnimated = ref(false)

const formattedCounters = computed(() =>
    counterItems.map((item, index) => {
      const value = counterRefs[index].value
      return item.value % 1 !== 0
          ? value.toFixed(1) + item.suffix
          : Math.round(value) + item.suffix
    })
)

let counterTimeline: gsap.core.Timeline | null = null

const { stop } = useIntersectionObserver(counterContainer, ([{isIntersecting}]) => {
  if (isIntersecting && !hasAnimated.value) {
    counterTimeline = gsap.timeline()

    counterItems.forEach((item, index) => {
      counterTimeline!.to(counterRefs[index], {
        value: item.value,
        duration: 2,
        ease: "power2.inOut",
      }, index * 0.2)
    })

    hasAnimated.value = true
    stop()
  }
}, {
  threshold: 0.3
})

onBeforeUnmount(() => {
  if (counterTimeline) {
    counterTimeline.kill()
  }
  stop()
})
</script>

<template>
  <div id="counter" class="padding-x-lg xl:mt-0 mt-32" ref="counterContainer">
    <div class="mx-auto grid-4-cols">
      <div
          class="bg-zinc-900 rounded-lg p-10 flex flex-col justify-center"
          v-for="(item, i) in counterItems"
          :key="i"
      >
        <div class="counter-number text-white text-5xl font-bold mb-2">
          {{ formattedCounters[i] }}
        </div>
        <div class="text-white-50 text-lg">{{ item.label }}</div>
      </div>
    </div>
  </div>
</template>