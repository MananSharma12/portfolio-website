<script setup lang="ts">
import { onMounted, nextTick } from "vue"
import gsap from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"
import { expCards } from "../constants"
import TitleHeader from "../components/TitleHeader.vue"
import GlowCard from "../components/GlowCard.vue"

gsap.registerPlugin(ScrollTrigger)

onMounted(async () => {
  await nextTick()

  gsap.utils.toArray('.timeline-card').forEach((card) => {
    gsap.from(card as Element, {
      xPercent: -100,
      opacity: 0,
      transformOrigin: 'left left',
      duration: 1,
      ease: 'power2.inOut',
      scrollTrigger: {
        trigger: card as Element,
        start: 'top 80%',
      }
    })
  })

  gsap.to('.timeline', {
    transformOrigin: 'bottom bottom',
    ease: 'power1.inOut',
    scrollTrigger: {
      trigger: '.timeline',
      start: 'top center',
      end: '70% center',
      onUpdate: (self) => {
        gsap.to('.timeline', {
          scaleY: 1 - self.progress,
        })
      }
    }
  })

  gsap.utils.toArray('.expText').forEach((text) => {
    gsap.from(text as Element, {
      opacity: 0,
      xPercent: 0,
      duration: 1,
      ease: 'power2.inOut',
      scrollTrigger: {
        trigger: text as Element,
        start: 'top 60%',
      }
    })
  })
})
</script>

<template>
  <section id="experience" class="w-full md:mt-40 mt-20">
    <div class="w-full h-full md:px-20 px-5">
      <TitleHeader title="Professional Work Experience" sub="💼 My career overview" />

      <div class="mt-32 relative">
        <div class="relative z-50 xl:space-y-32 space-y-10">
          <div
              v-for="card in expCards"
              :key="card.title"
              class="exp-card-wrapper"
          >
            <div class="xl:w-2/6">
              <GlowCard :card="card">
                <div>
                  <img :src="card.imgPath" :alt="card.title" />
                </div>
              </GlowCard>
            </div>
            <div class="xl:w-4/6">
              <div class="flex items-start">
                <div class="timeline-wrapper">
                  <div class="timeline" />
                  <div class="gradient-line w-1 h-full" />
                </div>

                <div class="expText flex xl:gap-20 md:gap-10 gap-5 relative z-20">
                  <div class="timeline-logo">
                    <img :src="card.logoPath" alt="logo" />
                  </div>
                  <div>
                    <h1 class="font-semibold text-3xl">{{ card.title }}</h1>
                    <p class="my-5 text-white-50">{{ card.date }}</p>
                    <p class="text-[#839cb5] italic">Responsibilities</p>
                    <ul class="list-disc ms-5 mt-5 flex flex-col gap-5 text-white-50">
                      <li
                          v-for="responsibility in card.responsibilities"
                          :key="responsibility"
                          class="text-lg"
                      >
                        {{ responsibility }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
