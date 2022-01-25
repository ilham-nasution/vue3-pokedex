<script setup>
import { defineProps } from "vue"

const props = defineProps({
  pokemonTypes: Array,
  pokemonStats: Array
})
</script>

<template>
  <div>
    <div class="flex mb-4">
      <p class="mr-2" v-for="pokemonType in pokemonTypes" :key="pokemonType.slot">{{pokemonType.type.name}}</p>
    </div>
    <h3 class="text-3xl mb-1">Base Stats:</h3>
    <div class="grid grid-cols-3">
      <p class="p-2 bg-white m-1 rounded-md shadow-sm" v-for="pokemonStat in pokemonStats" :key="pokemonStat.stat.name">{{pokemonStat.stat.name}}: {{pokemonStat.base_stat}}</p>
    </div>
  </div>
</template>