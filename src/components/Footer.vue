<script setup lang="ts">
import { isDark, toggleDark } from '~/logic'

const toggleMode = (payload: MouseEvent) => toggleDark()
</script>

<template>
  <nav class="mt-6 text-xl">
    <button class="mx-2 icon-btn !outline-none" @click="toggleMode">
      <carbon-moon v-if="isDark" />
      <carbon-sun v-else />
    </button>
  </nav>
</template>
