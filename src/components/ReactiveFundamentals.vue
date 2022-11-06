<template>
  <h1>{{ state.count }}</h1>

  <button @click="increment">Increment Count</button>
</template>

<script setup>
import { reactive } from 'vue'

const state = reactive({ count: 0 })
const increment = () => state.count++
</script>