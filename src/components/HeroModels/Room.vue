<script setup lang="ts">
import { useGLTF } from '@tresjs/cientos'

const { scene } = await useGLTF('/models/room.glb')
</script>

<template>
  <primitive :object="scene" />
</template>
