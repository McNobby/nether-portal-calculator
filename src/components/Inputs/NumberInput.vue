<script lang="ts" setup>
const id = Math.floor(Math.random() * 10000).toString(16)

const number = defineModel<number>({ required: true })

const { label, placeholder, vertical } = defineProps<{
  label: string
  placeholder?: string
  vertical?: boolean
}>()
</script>

<template>
  <div class="flex gap-3" :class="{ 'flex-col': vertical }">
    <label :for="id">{{ label }}</label>
    <input
      v-model.number="number"
      :placeholder
      class="bg-slate-700 p-1 rounded-md shadow"
      :id
      type="text"
    />
  </div>
</template>
