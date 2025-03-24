<script setup lang="ts">
import CommonCard from './components/CommonCard.vue'
import PortalCalculator from './components/PortalCalculator.vue'
</script>

<template>
  <main
    class="flex items-center justify-center h-screen bg-slate-900 flex-col gap-3 text-neutral-200"
  >
    <h1 class="text-5xl">Portal Calculator</h1>
    <CommonCard class="h-100 w-200">
      <PortalCalculator />
    </CommonCard>
  </main>
</template>

<style>
@import 'tailwindcss';
</style>
