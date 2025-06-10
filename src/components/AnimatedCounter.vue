<script setup lang="ts">
import { ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { gsap } from 'gsap'
import { counterItems } from '../constants'

const counterValues = ref(counterItems.map(() => 0))
const counterContainer = ref<HTMLElement>()
const hasAnimated = ref(false)

const { stop } = useIntersectionObserver(counterContainer, ([{isIntersecting}]) => {
  if (isIntersecting) {
    counterItems.forEach((item, index) => {
      gsap.to(counterValues.value, {
        [index]: item.value,
        duration: 2,
        ease: "power2.inOut",
        delay: index * 0.2,
      })
    })

    hasAnimated.value = true
    stop()
  }
}, {
  threshold: 0.3
})

const formatCounterValue = (value: number, suffix: string, targetValue: number) =>
    targetValue % 1 !== 0 ? value.toFixed(1) + suffix : Math.round(value) + suffix
</script>

<template>
  <div id="counter" class="padding-x-lg xl:mt-0 mt-32" ref="counterContainer">
    <div class="mx-auto grid-4-cols">
      <div
          class="bg-zinc-900 rounded-lg p-10 flex flex-col justify-center"
          v-for="(item, i) in counterItems"
          :key="i"
      >
        <div
            class="counter-number text-white text-5xl font-bold mb-2"
        >
          {{ formatCounterValue(counterValues[i], item.suffix, item.value) }}
        </div>
        <div class="text-white-50 text-lg">{{ item.label }}</div>
      </div>
    </div>
  </div>
</template>