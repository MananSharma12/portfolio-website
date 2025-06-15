<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { navLinks } from "../constants"

const scrolled = ref<boolean>(false)

const handleScroll = () => {
  scrolled.value = true
}

onMounted(() => {
  window.addEventListener("scroll", handleScroll)
})

onUnmounted(() => {
  if (handleScroll) {
    window.removeEventListener('scroll', handleScroll)
  }
})
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
        <div class="inner">
          <span>Contact Me</span>
        </div>
      </a>
    </div>
  </header>
</template>
