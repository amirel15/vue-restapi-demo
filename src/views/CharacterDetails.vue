<script setup>
import { onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

import useCharacters from '@/composables/useCharacters'

const route = useRoute()
const { fetchCharacter, currentCharacter } = useCharacters()

onMounted(async () => {
  await fetchCharacter(route.params.id)
})

onUnmounted(()=> {
  currentCharacter.value = null
})
</script>

<template>
  <main
    class="flex min-h-screen flex-col items-center justify-center gap-6 bg-gradient-to-br from-blue-900 to-teal-500 text-white"    
  >
  <div
      v-if="currentCharacter"
      class="flex flex-col items-center justify-center gap-6"
    >
      <img :src="currentCharacter.imageUrl" :alt="currentCharacter.name" />
      <h1 class="text-white-800 text-6xl font-semibold italic">
        Hello, I'm {{ currentCharacter.name }}
      </h1>
      <pre>{{ currentCharacter }}</pre>
    </div>
  </main>
</template>