<script setup lang="ts">
import CommonCard from '../CommonCard.vue'
import NumberInput from './NumberInput.vue'
import type iCoordinate from '@/interfaces/coordinate'

const { dimension } = defineProps<{
  dimension: string
}>()

const coords = defineModel<iCoordinate>({
  required: true,
})
</script>

<template>
  <CommonCard class="flex flex-col items-center content-center gap-3">
    <h3>{{ dimension }}</h3>
    <NumberInput v-model.number="coords.x" label="X:" />
    <NumberInput v-model.number="coords.y" label="Y:" />
    <NumberInput v-model.number="coords.z" label="Z:" />
  </CommonCard>
</template>
