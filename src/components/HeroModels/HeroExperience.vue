<script setup lang="ts">
import { TresCanvas } from "@tresjs/core"
import { OrbitControls } from "@tresjs/cientos"
import { useMediaQuery } from "@vueuse/core"
import Room from "./Room.vue"
import HeroLights from "./HeroLights.vue"
import Particles from "./Particles.vue";

const isTablet = useMediaQuery("(max-width: 1024px)")
const isMobile = useMediaQuery("(max-width: 768px)")
</script>

<template>
  <TresCanvas :camera="{ position: [0, 0, 15], fov: 45 }" >
    <OrbitControls
        :enable-pan="false"
        :enable-zoom="!isTablet"
        :min-distance="5"
        :max-distance="10"
        :min-polar-angle="Math.PI / 5"
        :max-polar-angle="Math.PI / 2"
    />
    <HeroLights />
    <Particles />
    <TresGroup
        :scale="isMobile ? 0.4 : 0.4"
        :position="[0, -1, 0]"
        :rotation="[0, -Math.PI / 7, 0]"
    >
      <Suspense>
        <Room />
      </Suspense>
    </TresGroup>
  </TresCanvas>
</template>
