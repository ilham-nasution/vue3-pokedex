<script setup>
  import { defineProps, ref } from "vue"

  const pokemonInput = ref("")

  const props = defineProps({
    pokemonSearch: Function
  })
</script>

<template>
  <form @submit.prevent="pokemonSearch(pokemonInput)">
    <input v-model="pokemonInput" class="focus:border-slate-500 focus:ring focus:ring-slate-400 focus:ring-opacity-50 rounded " type="search" name="pokemon" placeholder="search..."/>
    <button type="submit" class="bg-black rounded p-2 ml-2 text-white">Search</button>
  </form>
</template>