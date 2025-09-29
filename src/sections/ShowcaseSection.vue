<script setup lang="ts">
import { useTemplateRef, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { projectLinks } from "../constants";

gsap.registerPlugin(ScrollTrigger)

const sectionRef = useTemplateRef('section')
const project1Ref = useTemplateRef('project1')
const project2Ref = useTemplateRef('project2')

onMounted(() => {
  const cards = [project1Ref.value, project2Ref.value]

  gsap.fromTo(sectionRef.value, {
    opacity: 0,
  }, {
    opacity: 1,
    duration: 1.5,
  })

  cards.forEach((card, index) => {
    gsap.fromTo(card, {
      y:50,
      opacity: 0,
    }, {
      y: 0,
      opacity: 1,
      duration: 1,
      delay: 0.3 * (index + 1),
      scrollTrigger: {
        trigger: card,
        start: "top bottom-=100",
      }
    })
  })
})
</script>

<template>
  <section id="work" ref="section" class="app-showcase">
    <div class="w-full">
      <div class="showcaselayout">
      <!-- LEFT -->
        <div class="first-project-wrapper" ref="project1">
          <div class="image-wrapper">
            <img src="/images/project_heroforge.png" alt="HeroForge" />
          </div>
          <div class="text-content">
            <a :href="projectLinks.heroForge" target="_blank">
              <h2>HeroForge NFT</h2>
            </a>
            <p class="text-white-50 md:text-xl">An on-chain NFT card game where you can mint an ERC‑721 token with procedurally generated attributes and rarities. Players can mint heroes on Ethereum Sepolia testnet and view their collection in the frontend.</p>
          </div>
        </div>

        <!-- RIGHT -->
        <div class="first-project-wrapper xl:w-[35%]" ref="project2">
          <div class="image-wrapper">
            <img src="/images/project1.png" alt="TRI3D" />
          </div>
          <div class="text-content">
            <a :href="projectLinks.fab3d" target="_blank">
              <h2>Fab3D</h2>
            </a>
            <p class="text-white-50 md:text-xl">Fab3D, An innovative web application that seamlessly transforms fabric samples into stunning photorealistic visualizations.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>