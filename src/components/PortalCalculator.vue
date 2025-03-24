<template>
  <div class="flex flex-col w-full h-full items-center justify-center gap-3">
    <div class="flex">
      <CoordinateInput v-model="overworldCoordsModel" dimension="Overworld" />
      <!-- Bind to the computed property netherCoordsModel -->
      <CoordinateInput v-model="netherCoordsModel" dimension="Nether" />
    </div>
    <div>
      <TextInput
        v-model="command"
        :vertical="true"
        placeholder="/execute in..."
        label="Output from F3+C"
      ></TextInput>
    </div>
  </div>
</template>

<script setup lang="ts">
import CoordinateInput from './Inputs/CoordinateInput.vue'
import TextInput from './Inputs/TextInput.vue'
import { ref, watch, computed } from 'vue'

const command = ref('')

// Keep `netherCoords` reactive
const overworldCoords = ref({
  x: 0,
  y: 0,
  z: 0,
})

const netherCoords = ref({
  x: 0,
  y: 0,
  z: 0,
})

// Use computed for v-model handling
const netherCoordsModel = computed({
  get: () => netherCoords,
  set: (newValue) => {
    // Directly mutate the properties when setting
    netherCoords.value.x = newValue.value.x
    netherCoords.value.y = newValue.value.y
    netherCoords.value.z = newValue.value.z
  },
})

const overworldCoordsModel = computed({
  get: () => netherCoords,
  set: (newValue) => {
    // Directly mutate the properties when setting
    overworldCoords.value.x = newValue.value.x
    overworldCoords.value.y = newValue.value.y
    overworldCoords.value.z = newValue.value.z
  },
})

let stopNether = false
let stopOverworld = false

watch(netherCoords, (coords) => {
  if (stopNether) return

  stopOverworld = true

  overworldCoords.value.x = coords.x * 8
  overworldCoords.value.y = coords.y
  overworldCoords.value.z = coords.z * 8

  setTimeout(() => {
    stopOverworld = false
  }, 5)
})

watch(overworldCoords, (coords) => {
  if (stopOverworld) return

  stopNether = true

  netherCoords.value.x = Math.floor(coords.x / 8)
  netherCoords.value.y = coords.y
  netherCoords.value.z = Math.floor(coords.z / 8)

  setTimeout(() => {
    stopNether = false
  }, 5)
})

watch(command, (newCommand) => {
  const commandRegex = new RegExp(
    /\/execute in minecraft:(overworld|nether) run tp @s ((-?\d+(\.\d+)?\s){3})-?\d+(\.\d+)?\s-?\d+(\.\d+)?/,
  )

  if (!commandRegex.test(newCommand)) return

  const result = commandRegex.exec(newCommand)
  if (!result) return
  if (!result[1]) return
  if (!result[2]) return

  const dimension = result[1]
  const newCoords = result[2] as string

  const [x, y, z] = newCoords.split(' ')

  if (dimension === 'overworld') {
    overworldCoords.value.x = parseInt(x)
    overworldCoords.value.y = parseInt(y)
    overworldCoords.value.z = parseInt(z)
  } else {
    netherCoords.value.x = parseInt(x)
    netherCoords.value.y = parseInt(y)
    netherCoords.value.z = parseInt(z)
  }
})
</script>
