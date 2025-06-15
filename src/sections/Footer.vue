<script setup lang="ts">
import { socialImgs } from "../constants";
</script>

<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="flex flex-col justify-center md:items-start items-center">
<!--        <a href="/">Visit my blog</a>-->
      </div>

      <div class="socials">
        <a
            v-for="(img, i) in socialImgs"
            :key="i"
            class="icon"
            :href="img.url"
            target="_blank"
        >
          <img :src="img.imgPath" :alt="img.name" />
        </a>
      </div>

      <div class="flex flex-col justify-center">
        <p class="text-center md:text-end">
          © {{ new Date().getFullYear() }} Manan Sharma. All rights reserved.
        </p>
      </div>
    </div>
  </footer>
</template>
