<script setup lang="ts">
import CommonCard from './components/CommonCard.vue'
import PortalCalculator from './components/PortalCalculator.vue'
import TutorialCard from './components/TutorialCard.vue'
</script>

<template>
  <main
    class="flex items-center justify-center h-screen bg-slate-900 flex-col gap-3 text-neutral-200"
  >
    <h1 class="text-5xl">Portal Calculator</h1>

    <div class="flex flex-col items-center justify-center">
      <CommonCard class="h-full w-full">
        <PortalCalculator />
      </CommonCard>
      <TutorialCard class="w-full h-full" />
    </div>
  </main>
</template>

<style>
@import 'tailwindcss';
</style>
