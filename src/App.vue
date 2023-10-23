<script setup lang="ts">
import NestedList from './components/NestedList.vue'
import SortList from './components/SortList.vue'

import { ref } from 'vue'

const listsProps = ref([
  {
    id: 0,
    name: 'List 1',
    items: [
      { id: 5, name: 'Item 1', count: 10, color: '#0040ff', selected: true },
      { id: 6, name: 'Item 2', count: 18, color: '#ff0a0a', selected: true },
      { id: 7, name: 'Item 3', count: 32, color: '#2eff6d', selected: true },
      { id: 8, name: 'Item 4', count: 8, color: '#bc05ff', selected: true },
    ],
    sorted: true,
    opened: false,
  },
  {
    id: 1,
    name: 'List 2',
    items: [
      { id: 9, name: 'Item 1', count: 10, color: '#0040ff', selected: true },
      { id: 10, name: 'Item 2', count: 18, color: '#ff0a0a', selected: true },
      { id: 11, name: 'Item 3', count: 32, color: '#2eff6d', selected: false },
      { id: 12, name: 'Item 4', count: 8, color: '#bc05ff', selected: false },
    ],
    sorted: true,
    opened: false,
  },
  {
    id: 2,
    name: 'List 3',
    items: [
      { id: 13, name: 'Item 1', count: 10, color: '#0040ff', selected: false },
      { id: 14, name: 'Item 2', count: 18, color: '#ff0a0a', selected: false },
      { id: 15, name: 'Item 3', count: 32, color: '#2eff6d', selected: false },
      { id: 16, name: 'Item 4', count: 8, color: '#bc05ff', selected: false },
    ],
    sorted: true,
    opened: false,
  },
  {
    id: 3,
    name: 'List 4',
    items: [
      { id: 17, name: 'Item 1', count: 10, color: '#0040ff', selected: false },
      { id: 18, name: 'Item 2', count: 18, color: '#ff0a0a', selected: false },
      { id: 19, name: 'Item 3', count: 32, color: '#2eff6d', selected: false },
      { id: 20, name: 'Item 4', count: 8, color: '#bc05ff', selected: false },
    ],
    sorted: true,
    opened: false,
  },
  {
    id: 4,
    name: 'List 5',
    items: [
      { id: 21, name: 'Item 1', count: 10, color: '#0040ff', selected: false },
      { id: 22, name: 'Item 2', count: 18, color: '#ff0a0a', selected: false },
      { id: 23, name: 'Item 3', count: 32, color: '#2eff6d', selected: false },
      { id: 24, name: 'Item 4', count: 8, color: '#bc05ff', selected: false },
    ],
    sorted: true,
    opened: false,
  },
])
</script>

<template>
  <div class="wrapper">
    <NestedList :lists="listsProps" />
    <SortList :lists="listsProps" />
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  gap: 30px;
  justify-content: center;
  margin-top: 60px;
}
</style>
