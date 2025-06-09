<script setup lang="ts">
import { ref, computed, type Ref } from 'vue'
import { useRenderLoop } from '@tresjs/core'
import type { Points, BufferGeometry } from 'three'

interface Particle {
  position: [number, number, number]
  speed: number
}

const props = withDefaults(defineProps<{
  count?: number
}>(), {
  count: 200
})

const meshRef: Ref<Points<BufferGeometry> | undefined> = ref()

const particles = computed<Particle[]>(() => {
  const temp: Particle[] = []
  for (let i = 0; i < props.count; i++) {
    temp.push({
      position: [
        (Math.random() - 0.5) * 10,
        Math.random() * 10 + 5,
        (Math.random() - 0.5) * 10,
      ],
      speed: 0.005 + Math.random() * 0.001,
    })
  }
  return temp
})

const positions = computed<Float32Array>(() => {
  const positionsArray = new Float32Array(props.count * 3)
  particles.value.forEach((p, i) => {
    positionsArray[i * 3] = p.position[0]
    positionsArray[i * 3 + 1] = p.position[1]
    positionsArray[i * 3 + 2] = p.position[2]
  })
  return positionsArray
})

const { onLoop } = useRenderLoop()

onLoop(() => {
  if (!meshRef.value) return

  const positionsArray = meshRef.value.geometry.attributes.position.array as Float32Array

  for (let i = 0; i < props.count; i++) {
    let y = positionsArray[i * 3 + 1]
    y -= particles.value[i].speed
    if (y < -2) y = Math.random() * 10 + 5
    positionsArray[i * 3 + 1] = y
  }

  meshRef.value.geometry.attributes.position.needsUpdate = true
})
</script>

<template>
  <TresPoints ref="meshRef">
    <TresBufferGeometry>
      <TresBufferAttribute
          :args="[positions, 3]"
          attach="attributes-position"
          :count="count"
      />
    </TresBufferGeometry>
    <TresPointsMaterial
        color="white"
        :size="0.05"
        :transparent="true"
        :opacity="0.9"
        :depth-write="false"
    />
  </TresPoints>
</template>
