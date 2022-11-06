<template>
  <ShoppingList />

  <ReactiveFundamentals />
</template>

<script>
import ShoppingList from './components/ShoppingList.vue'
import ReactiveFundamentals from './components/ReactiveFundamentals.vue'

export default {
  name: 'App',

  components: {
    ShoppingList,
    ReactiveFundamentals
  }
}
</script>

