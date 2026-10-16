<script setup lang="ts">
import { computed } from "vue";
import { useWindowScroll } from "@vueuse/core";
import { navLinks, RESUME } from "../constants";

const { y } = useWindowScroll();
const scrolled = computed(() => y.value > 10);
</script>

<template>
  <header :class="`navbar ${ scrolled ? 'scrolled': 'not-scrolled' }`">
    <div class="inner">
      <a class="logo" href="#hero">Manan Sharma</a>

      <nav class="desktop">
        <ul>
          <li v-for="{ link, name } in navLinks">
            <a :href="link">
              <span>{{ name }}</span>
            </a>
          </li>
        </ul>
      </nav>

      <a href="#contact" class="contact-btn group">
        <div class="mt-2 mr-4 underline">
          <a :href="RESUME" target="_blank">
            <span>Résumé</span>
          </a>
        </div>

        <div class="inner">
          <span>Contact Me</span>
        </div>
      </a>
    </div>
  </header>
</template>
