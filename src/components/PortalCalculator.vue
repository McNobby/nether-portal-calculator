<template>
  <div class="flex flex-col w-full h-full items-center justify-center gap-3">
    <div class="flex">
      <CoordinateInput v-model="overworldCoords" dimension="Overworld" />
      <CoordinateInput v-model="netherCoords" dimension="Nether" />
    </div>
    <div>
      <TextInput
        v-model="command"
        :vertical="true"
        placeholder="/execute in..."
        label="Output from F3+C"
      ></TextInput>

      {{ overworldCoords }}
      {{ netherCoords }}
    </div>
  </div>
</template>

<script setup lang="ts">
import CoordinateInput from './Inputs/CoordinateInput.vue'
import TextInput from './Inputs/TextInput.vue'
import { reactive, ref, watch } from 'vue'

const command = ref('')

const overworldCoords = reactive({
  x: 0,
  y: 0,
  z: 0,
})

const netherCoords = reactive({
  x: 0,
  y: 0,
  z: 0,
})

let stopNether = false
let stopOverworld = false

watch(netherCoords, (coords) => {
  if (stopNether) return

  stopOverworld = true

  overworldCoords.x = coords.x * 8
  overworldCoords.y = coords.y
  overworldCoords.z = coords.z * 8

  setTimeout(() => {
    stopOverworld = false
  }, 5)
})

watch(overworldCoords, (coords) => {
  if (stopOverworld) return

  stopNether = true

  netherCoords.x = Math.floor(coords.x / 8)
  netherCoords.y = coords.y
  netherCoords.z = Math.floor(coords.z / 8)

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
    overworldCoords.x = parseInt(x)
    overworldCoords.y = parseInt(y)
    overworldCoords.z = parseInt(z)
  } else {
    netherCoords.x = parseInt(x)
    netherCoords.y = parseInt(y)
    netherCoords.z = parseInt(z)
  }
})
</script>
