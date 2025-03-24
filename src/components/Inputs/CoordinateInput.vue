<script setup lang="ts">
import CommonCard from '../CommonCard.vue'
import { reactive } from 'vue'
import NumberInput from './NumberInput.vue'

const { dimension } = defineProps<{
  dimension: string
}>()

const model = defineModel({
  default: {
    x: 0,
    y: 0,
    z: 0,
  },
})

const coords = reactive(model)
</script>

<template>
  <CommonCard class="flex flex-col items-center content-center gap-3">
    <h3>{{ dimension }}</h3>
    <NumberInput v-model.number="coords.x" label="X:" />
    <NumberInput v-model.number="coords.y" label="Y:" />
    <NumberInput v-model.number="coords.z" label="Z:" />
  </CommonCard>
</template>
