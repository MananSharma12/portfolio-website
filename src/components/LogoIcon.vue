<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  imgPath: string
  name?: string
}>()

const imgRef = ref<HTMLImageElement>()
const loaded = ref(false)
const error = ref(false)

const handleLoad = () => {
  loaded.value = true
}

const handleError = () => {
  error.value = true
  console.warn(`Failed to load logo: ${props.imgPath}`)
}

onMounted(() => {
  const img = new Image()
  img.onload = handleLoad
  img.onerror = handleError
  img.src = props.imgPath
})
</script>

<template>
  <div class="flex-none flex-center marquee-item">
    <img
        ref="imgRef"
        :src="imgPath"
        alt="Company logo"
        loading="lazy"
        decoding="async"
        class="max-w-40 max-h-40 object-contain"
        @load="handleLoad"
        @error="handleError"
    />
  </div>
</template>
