<script setup lang="ts">
import { ref, computed } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, lable: '10 party hats', purchased: true, highPriority: true },
  { id: 2, lable: '2 board games', purchased: true, highPriority: false },
  { id: 3, lable: '20 cups', purchased: false, highPriority: true },
  // { id: 4, lable: '420 bread' },
])
const reversedItems = computed(() => {
  return [...items.value].reverse() // reversed array
})
const newItem = ref('')
const editing = ref(false)
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    lable: newItem.value,
    purchased: false,
    highPriority: newItemHighPriority.value,
  })
  newItem.value = ''
  newItemHighPriority.value = false
}
const doEdit = (e: boolean) => {
  editing.value = e
  newItem.value = ''
  newItemHighPriority.value = false
}

const togglePurchased = (item: { purchased: boolean }) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
  </div>
  <form class="add-item-form" v-if="editing" @submit.prevent="saveItem">
    <input v-model.trim="newItem" type="text" placeholder="Add an Item" />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button v-bind:disabled="newItem.length < 5" class="btn btn-primary">Save Item</button>
  </form>
  <ul>
    <li
      v-for="item in reversedItems"
      @click="togglePurchased(item)"
      class="static-class"
      :key="item.id"
      :class="{ strikeout: item.purchased, priority: item.highPriority }"
    >
      {{ item.lable }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>

<style lang="css">
@import './main.css';
</style>
