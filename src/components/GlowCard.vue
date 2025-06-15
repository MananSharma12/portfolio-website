<script setup lang="ts">
import { ref } from "vue";

interface Card {
  review: string;
  author: string;
  imgPath: string;
  logoPath: string;
  title: string;
  date: string;
  responsibilities: string[];
}

const { card } = defineProps<{
  card: Card
}>()

const cardRef = ref<HTMLDivElement | null>(null)

const handleMouseMove = (e: MouseEvent) => {
  const card = cardRef.value
  if (!card) return

  const rect = card.getBoundingClientRect()
  const mouseX = e.clientX - rect.left - rect.width / 2
  const mouseY = e.clientY - rect.top - rect.height / 2

  let angle = Math.atan2(mouseY, mouseX) * (180 / Math.PI)

  angle = (angle + 360) % 360

  card.style.setProperty('--start', (angle + 60).toString())
}
</script>

<template>
  <div
      ref="cardRef"
      @mousemove="handleMouseMove"
      class="card card-border timeline-card rounded-xl p-10"
  >
    <div class="glow" />
    <div class="mb-5">
      <p class="text-white-50 text-lg">
        {{ card.review }}
      </p>
      <p class="text-white-50 italic mt-2 text-right">- {{ card.author }}</p>
    </div>
    <slot></slot>
  </div>
</template>
