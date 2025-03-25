<script lang="ts" setup>
const id = Math.floor(Math.random() * 10000).toString(16)

const text = defineModel<string>({ required: true })

const { label, placeholder, vertical } = defineProps<{
  label: string
  placeholder?: string
  vertical?: boolean
}>()
</script>

<template>
  <div class="flex gap-3 w-full" :class="{ 'flex-col': vertical }">
    <label :for="id">{{ label }}</label>
    <input
      v-model="text"
      :placeholder
      class="bg-slate-700 p-1 rounded-md shadow w-full"
      :id
      type="text"
    />
  </div>
</template>
