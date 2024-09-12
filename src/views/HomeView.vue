<script setup lang="ts">
import SpinePlayer from '@/components/SpinePlayer.vue'
import { ref } from 'vue'

const size = ref(100)
</script>

<template>
  <main>
    <SpinePlayer :width="size + 'px'" :height="size + 'px'" />
    <button @click="size += 100">add size</button>
  </main>
</template>
<style scoped></style>
