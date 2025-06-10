<script setup lang="ts">
import { useTemplateRef, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger)

const sectionRef = useTemplateRef('section')
const project1Ref = useTemplateRef('project1')
const project2Ref = useTemplateRef('project2')
const project3Ref = useTemplateRef('project3')

onMounted(() => {
  const cards = [project1Ref.value, project2Ref.value, project3Ref.value]

  gsap.fromTo(sectionRef, {
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
            <img src="/images/project1.png" alt="TRI3D" />
          </div>
          <div class="text-content">
            <h2>Get visualization for your fabric on photorealistic models in just 2 clicks with Fab3D!</h2>
            <p class="text-white-50 md:text-xl">Fab3D, An innovative web application that seamlessly transforms fabric samples into stunning photorealistic visualizations.</p>
          </div>
        </div>

      <!-- RIGHT -->
        <div class="project-list-wrapper overflow-hidden">
          <div class="project" ref="project2">
            <div class="image-wrapper bg-[#ffefdb]">
              <img src="/images/project1.png" alt="TRI3D" />
              <h2>Fab3D</h2>
            </div>
          </div>

          <div class="project" ref="project3">
            <div class="image-wrapper bg-[#ffe7db]">
              <img src="/images/project1.png" alt="TRI3D" />
              <h2>Fab3D</h2>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>