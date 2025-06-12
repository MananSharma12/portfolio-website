<script setup lang="ts">
import { logoIconsList } from "../constants";
import LogoIcon from "../components/LogoIcon.vue";
</script>

<template>
  <div class="md:my-20 my-10 relative">
    <div class="gradient-edge" />
    <div class="gradient-edge" />

    <div class="marquee h-52">
      <div class="marquee-box md:gap-12 gap-5">
        <LogoIcon
            v-for="({ imgPath }, index) in logoIconsList"
            :key="index"
            :imgPath="imgPath"
        />

        <LogoIcon
            v-for="({ imgPath }, index) in logoIconsList"
            :key="`duplicate-${index}`"
            :imgPath="imgPath"
        />
      </div>
    </div>
  </div>
</template>