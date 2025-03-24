<template>
  <CommonCard>
    <div class="text-center p-4">
      <h2 class="text-xl font-bold mb-2">Minecraft Portal Guide 🏗️</h2>
      <p class="mb-4">
        Want to link portals between the Overworld 🌍 and the Nether 🔥? Here’s how:
      </p>
      <ul class="mb-4 text-left inline-block">
        <li>1️⃣ Place a Nether portal in the Overworld where you want it.</li>
        <li>2️⃣ Enter the X and Z coordinates into the Overworld input.</li>
        <li>3️⃣ The Nether coordinates will update automatically! 📍</li>
        <li>4️⃣ Go to the Nether and build a portal at the calculated spot.</li>
        <li>Light it up and step through! ✨</li>
      </ul>
      <p>
        ⚡You can also paste the result from pressing <code>F3+C</code> to auto-fill coordinates.
      </p>
    </div>
  </CommonCard>
</template>

<script setup lang="ts">
import CommonCard from './CommonCard.vue'
</script>
