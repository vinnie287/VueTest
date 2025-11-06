<script setup lang="ts">
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, lable: '10 party hats' },
  { id: 2, lable: '2 board games' },
  { id: 3, lable: '20 cups' },
  { id: 4, lable: '420 bread' },
])
const newItem = ref('')
const newItemHighPriority = ref(false)
</script>

<template>
  <h1>{{ header }}</h1>
  <input v-model.trim="newItem" type="text" placeholder="Add an Item" />
  Priority:
  <label>
    <input type="checkbox" v-model="newItemHighPriority" />
    High Priority
  </label>
  <ul>
    <li v-for="{ id, lable } in items" :key="id">
      {{ lable }}
    </li>
  </ul>
</template>

<style lang="css">
@import './main.css';
</style>
