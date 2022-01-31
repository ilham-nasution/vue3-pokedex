<script setup>
  import axios from "axios"
  import { ChevronUpIcon, ChevronDownIcon } from "@heroicons/vue/outline"
  import { ref, computed, watchEffect } from "vue";
  import Title from "./components/Title.vue"
  import Stats from "./components/Stats.vue"

  const pokemon = ref({})
  const pokemonImg = ref("")
  const pokemonTypes = ref([])
  const pokemonStats = ref([])
  const page = ref(1)

  const fetchPokemon = async (page) => {
    const req = await axios.get(`https://pokeapi.co/api/v2/pokemon/${page}/`)
    pokemon.value = req.data
    pokemonImg.value = req.data.sprites.other.dream_world.front_default
    pokemonTypes.value = req.data.types
    pokemonStats.value = req.data.stats
  }

  watchEffect(() => {
    fetchPokemon(page.value)
  })

  const pokemonNum = computed(() => {
    if(pokemon.value.id?.toString().length === 1) {
      return `00${pokemon.value.id}`
    } else if(pokemon.value.id?.toString().length === 2) {
      return `0${pokemon.value.id}`
    } else {
      return `${pokemon.value.id}`
    }
  })

  const goToPage = (event) => {
    fetchPokemon(event.target.innerText)
  }

  const prevPage = () => {
    if(page.value > 1) {
      page.value --
    }
  }
</script>

<template>
  <div class="bg-gray-300 w-screen h-screen">
    <div class="p-14">
      <Title :name="pokemon.name" :num="pokemonNum" />
      <div class="flex justify-around items-center h-96">
        <div class="w-36">
          <h3>Height: {{pokemon.height}}m</h3>
          <h3>Weight: {{pokemon.weight}}kg</h3>
        </div>
        <img :src="pokemonImg" :alt="pokemon.name"  class="w-72"/>
        <Stats :pokemonTypes="pokemonTypes" :pokemonStats="pokemonStats" />
        <div class="flex flex-col items-center text-lg w-5">
          <ChevronUpIcon @click="prevPage" class="h-7 hover:h-8 cursor-pointer" />
          <div @click="goToPage" class="hover:text-xl cursor-pointer" v-for="num in [...Array(10).keys()]" :key="num">
            {{num + page}}
          </div>
          <ChevronDownIcon @click="page++" class="h-7 hover:h-8 cursor-pointer" />
        </div>
      </div>
      <h3 class="-rotate-90 -translate-x-[40rem] -translate-y-[38rem]">Region: Kanto</h3>
    </div>
  </div>
</template>
