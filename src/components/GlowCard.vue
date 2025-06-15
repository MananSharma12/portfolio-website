<script setup lang="ts">
import { ref, computed } from "vue";
import { useMouseInElement, useRafFn } from "@vueuse/core";

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
  card: Card;
}>();

const cardRef = ref<HTMLDivElement | null>(null);

const { elementX, elementY, isOutside, elementHeight, elementWidth } = useMouseInElement(cardRef);

const angle = computed(() => {
  if (isOutside.value) return 0;

  const centerX = elementWidth.value / 2;
  const centerY = elementHeight.value / 2;
  const dx = elementX.value - centerX;
  const dy = elementY.value - centerY;
  const rad = Math.atan2(dy, dx);
  let deg = rad * (180 / Math.PI);
  return (deg + 360) % 360;
});

useRafFn(() => {
  if (cardRef.value && !isOutside.value) {
    cardRef.value.style.setProperty("--start", (angle.value + 60).toString());
  }
});
</script>

<template>
  <div
      ref="cardRef"
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
