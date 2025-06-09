<script setup lang="ts">
import { words } from "../../constants";
import Button from "../Button.vue";
import HeroExperience from "../HeroModels/HeroExperience.vue";
</script>

<template>
  <section id="hero" class="relative overflow-hidden">
    <div class="absolute top-0 left-0 z-10">
      <img src="/images/bg.png" alt="background" />
    </div>

    <div class="hero-layout">
      <!-- LEFT: HERO CONTENT -->
      <header class="flex flex-col justify-center md:w-full w-screen md:px-20 px-5">
        <div class="hero-text">
          <h1>
            Shaping
            <span class="slide">
              <span class="wrapper">
                <span v-for="word in words" class="flex items-center md:gap-3 gap-1 pb-2">
                  <img
                      :src="word.imgPath"
                      :alt="word.text"
                      class="xl:size-12 md:size-10 size-7 md:p-2 p-1 rounded-full bg-white-50"
                  >
                  <span>{{ word.text }}</span>
                </span>
              </span>
            </span>
          </h1>
          <h1>into Real Projects</h1>
          <h1>that Deliver Results</h1>
        </div>
        <p class="text-white-50 md:text-xl relative z-10 pointer-events-none">
          Hi, I'm Manan, a Frontend Developer based in 🇮🇳.
        </p>
        <Button class-name="md:w-80 md:h-16 w-60 h-12 md:mt-6 mt-3" id="button" text="See my work!" />
      </header>

      <!-- RIGHT: 3D MODEL -->
      <figure>
        <div class="hero-3d-layout">
          <HeroExperience />
        </div>
      </figure>
    </div>
  </section>
</template>
