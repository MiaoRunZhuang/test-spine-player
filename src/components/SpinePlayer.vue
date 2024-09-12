<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'
import spine from '@/lib/spine-player/spine-player'

const { width = '200px', height = '200px' } = defineProps<{
  width: string
  height: string
}>()

const spineContainerRef = ref<HTMLElement>(null)

const spinePlayerInstance = ref<spine.SpinePlayer>(null)

function updateSpinePlayerView() {
  if (!spinePlayerInstance.value) return
  spinePlayerInstance.value.canvas.style.width = width
  spinePlayerInstance.value.canvas.style.height = height
  spinePlayerInstance.value.playerControls.style.display = 'none'
}

watch(() => [width, height], updateSpinePlayerView)

onMounted(() => {
  spinePlayerInstance.value = new spine.SpinePlayer(spineContainerRef.value, {
    jsonUrl: './spine/pet_12/pet_12.json',
    atlasUrl: './spine/pet_12/pet_12.atlas',
    animation: 'idle',
    showControls: false,
    premultipliedAlpha: true,
    backgroundColor: '#00000000',
    alpha: true,
    defaultMix: 1,
    success: (player) => {
      spinePlayerInstance.value = player
      updateSpinePlayerView()
    }
  })
  updateSpinePlayerView()
})
</script>

<template>
  <div ref="spineContainerRef"></div>
</template>
