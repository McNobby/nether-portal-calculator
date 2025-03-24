<script setup lang="ts">
import TextInput from './TextInput.vue'
import CommonCard from '../CommonCard.vue'
import { reactive } from 'vue'

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
    <TextInput v-model="coords.x" label="X:" />
    <TextInput v-model="coords.y" label="Y:" />
    <TextInput v-model="coords.z" label="Z:" />
  </CommonCard>
</template>
