<script setup lang="ts">
import CommonCard from './components/CommonCard.vue'
import PortalCalculator from './components/PortalCalculator.vue'
import TutorialCard from './components/TutorialCard.vue'
</script>

<template>
  <main
    class="flex h-full md:h-screen items-center justify-center bg-slate-900 flex-col gap-3 text-neutral-200 pt-10 pb-10"
  >
    <h1 class="text-4xl">Portal Calculator</h1>

    <div class="flex flex-col items-center justify-center w-full px-4 md:w-xl lg:w-3xl">
      <CommonCard
        class="h-full w-full drop-shadow-portal hover:drop-shadow-portal-lg transition transition-150"
      >
        <PortalCalculator />
      </CommonCard>
      <TutorialCard class="w-full h-full" />
    </div>

    <div class="text-center">
      <i
        >Created by
        <a href="https://github.com/McNobby" target="_blank" class="font-bold"> @TeoBB </a>
      </i>
      <p>2025</p>
    </div>
  </main>
</template>

<style>
@import 'tailwindcss';

@theme {
  --drop-shadow-portal: 0 -15px 25px rgba(154, 16, 204, 0.2);
  --drop-shadow-portal-lg: 0 -15px 55px rgba(154, 16, 204, 0.25);
}
</style>
