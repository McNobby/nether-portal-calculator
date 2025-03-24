<script lang="ts" setup>
const id = Math.floor(Math.random() * 10000).toString(16)

const text = defineModel({ required: true })

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
      v-model.number="text"
      :placeholder
      class="bg-slate-700 p-1 rounded-md shadow"
      :id
      type="number"
    />
  </div>
</template>
