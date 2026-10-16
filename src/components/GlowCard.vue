<script setup lang="ts">
import { ref, computed } from "vue";
import { useMouseInElement } from "@vueuse/core";

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

const { elementX, elementY, isOutside, elementHeight, elementWidth } = useMouseInElement(cardRef, {
  target: cardRef,
  handleOutside: false,
  windowScroll: false,
  touch: false,
});

const startAngle = computed(() => {
  if (isOutside.value) return 0;

  const centerX = elementWidth.value / 2;
  const centerY = elementHeight.value / 2;
  const dx = elementX.value - centerX;
  const dy = elementY.value - centerY;
  const rad = Math.atan2(dy, dx);
  const deg = (rad * (180 / Math.PI) + 360) % 360;
  return deg + 60;
});
</script>

<template>
  <div
      ref="cardRef"
      :style="{ '--start': startAngle }"
      class="card card-border timeline-card rounded-xl p-10"
  >
    <div class="mb-5">
      <p class="text-white-50 text-lg">
        {{ card.review }}
      </p>
      <p class="text-white-50 italic mt-2 text-right">
        <span v-if="card.author">- {{ card.author }}</span>
      </p>
    </div>
    <slot></slot>
  </div>
</template>
