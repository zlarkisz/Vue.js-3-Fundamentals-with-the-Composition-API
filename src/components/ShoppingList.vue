<template>
<div class="header">
  <h1>{{ header }}</h1>

  <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
  <button v-else class="btn btn-primary"  @click="doEdit(true)">Abb item</button>
</div>

<form v-if="editing" class="add-item-form" @submit.prevent="saveItem">
  <input
    v-model.trim="newItem"
    type="text"
    placeholder="Add an item"
  >

  <label>
    <input v-model="newItemHighPriority" type="checkbox">
    High priority
  </label>

  <button
    :disabled="newItem.length < 5"
    type="submit"
    class="btn btn-primary"
  >
    Save Item
  </button>
</form>

<ul>
  <li
    v-for="item in reversedItems"
    :key="item.id"
    :class="{
      strikeout: item.puchased,
      priority: item.highPriority,
      'static-class': true
    }"
    @click="togglePurhased(item)"
  >
    {{ item.label }}
  </li>
</ul>

<p v-if="!items.length">
  Nothing to see here
</p>
</template>

<script setup>
import { ref, computed } from 'vue'

const header = ref('Shopping List App')
const editing = ref(false)
const items = ref([
  {
    id: 1,
    label: "10 party hats",
    puchased: true,
    highPriority: false
  },
  {
    id: 2,
    label:"2 board games",
    puchased: true,
    highPriority: false
  },
  {
    id: 3,
    label: "20 cups",
    puchased: false,
    highPriority: true
  }
])
const reversedItems = computed(() => [...items.value].reverse())
const newItem = ref('')
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    highPriority: newItemHighPriority.value,
  })
  newItem.value = ''
  newItemHighPriority.value = ''
}
const doEdit = (e) => {
  editing.value = e
  newItem.value = ''
  newItemHighPriority.value = ''
}
const togglePurhased = item => item.puchased = !item.puchased
</script>
