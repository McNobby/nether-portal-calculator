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
    </div>
  </div>
</template>

<script setup lang="ts">
import CoordinateInput from './Inputs/CoordinateInput.vue'
import TextInput from './Inputs/TextInput.vue'
import { ref, watch, watchEffect } from 'vue'

const command = ref('')

const overworldCoords = ref({ x: 0, y: 0, z: 0 })
const netherCoords = ref({ x: 0, y: 0, z: 0 })

let stopNether = false
let stopOverworld = false

watch(
  overworldCoords,
  (coords) => {
    if (stopOverworld) return
    stopNether = true

    netherCoords.value.x = Math.floor(coords.x / 8)
    netherCoords.value.y = coords.y
    netherCoords.value.z = Math.floor(coords.z / 8)

    setTimeout(() => {
      stopNether = false
    }, 5)
  },
  { deep: true },
)

watch(
  netherCoords,
  (coords) => {
    if (stopNether) return
    stopOverworld = true

    overworldCoords.value.x = coords.x * 8
    overworldCoords.value.y = coords.y
    overworldCoords.value.z = coords.z * 8

    setTimeout(() => {
      stopOverworld = false
    }, 5)
  },
  { deep: true },
)
watchEffect(parseCommand)

function parseCommand() {
  const commandRegex = new RegExp(
    /\/execute in minecraft:(overworld|nether) run tp @s ((-?\d+(\.\d+)?\s){3})-?\d+(\.\d+)?\s-?\d+(\.\d+)?/,
  )

  console.log('here', commandRegex.test(command.value), commandRegex.exec(command.value))
  if (!commandRegex.test(command.value)) return

  const result = commandRegex.exec(command.value)
  if (!result) return
  if (!result[1]) return
  if (!result[2]) return

  console.log('here too')

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
}
</script>
