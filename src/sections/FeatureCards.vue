<script setup lang="ts">
import { abilities } from "../constants";
</script>

<template>
  <div class="w-full padding-x-lg">
    <div class="mx-auto grid-3-cols">
      <div
          v-for="{ imgPath, title, desc } in abilities"
          :key="title"
          class="card-border rounded-xl p-8 flex flex-col gap-4"
      >
        <div class="size-14 flex items-center justify-center rounded-full">
          <img :src="imgPath" :alt="title" />
        </div>
        <h3 class="text-white text-2xl font-semibold mt-2">{{ title }}</h3>
        <p class="text-white-50 text-lg">{{ desc }}</p>
      </div>
    </div>
  </div>
</template>
