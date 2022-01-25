<script setup>
import { defineProps } from "vue"

const props = defineProps({
  name: String,
  num: String
})
</script>

<template>
  <div class="mb-8">
    <h1 class="text-5xl">#{{num}}</h1>
    <h1 class="text-5xl capitalize">{{name}}</h1>
  </div>
</template>
