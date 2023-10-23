<script setup lang="ts">
import { ListProps } from './NestedList.vue'
import { ListItemType } from './ListItem.vue'

defineProps<{ lists: ListProps[] }>()

const selectedItems = (items: ListItemType[]) => {
  return items.filter((item) => {
    return item.selected
  })
}

const shuffleItems = (items: ListItemType[]) => {
  const filter = items.filter((item) => {
    return item.selected
  })

  const array: ListItemType[] = []

  filter.forEach((value) => {
    for (let index = 1; index <= value.count; index++) {
      array.push(value)
    }
  })

  for (let i = array.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1)) // случайный индекс от 0 до i
    ;[array[i], array[j]] = [array[j], array[i]]
  }

  return array
}
</script>

<template>
  <section class="sort-list">
    <div v-for="list in lists" :key="list.id" class="sort-list__item">
      <span>{{ list.name }}</span>
      <button
        v-if="selectedItems(list.items).length"
        class="sort-list__button"
        @click="
          () => {
            list.sorted = !list.sorted
          }
        "
      >
        {{ list.sorted ? 'Перемешать' : 'Сортировать' }}
      </button>

      <div v-if="selectedItems(list.items).length && list.sorted" class="sort-list__squares">
        <div v-for="item in selectedItems(list.items)" :key="item.id" class="sort-list__group">
          <div
            v-for="(_, index) in item.count"
            :key="index"
            class="sort-list__square"
            :style="{ backgroundColor: item.color }"
          />
        </div>
      </div>

      <div
        v-if="selectedItems(list.items).length && !list.sorted"
        class="sort-list__squares"
        :style="{ flexDirection: 'row', flexWrap: 'wrap' }"
      >
        <div
          v-for="(square, index) in shuffleItems(list.items)"
          :key="index"
          class="sort-list__square"
          :style="{ backgroundColor: square.color }"
        />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.sort-list {
  user-select: none;
  width: fit-content;
  min-width: 420px;
  max-width: 420px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding: 20px 10px;
  border: 1px solid #a3a3a3;

  &__item {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 5px;
    border: 1px solid #a3a3a3;
  }

  &__button {
    cursor: pointer;
    background-color: lightskyblue;
    border: 1px solid #636363;
    border-radius: 4px;
    padding: 4px;
    margin-bottom: 4px;
  }

  &__squares {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  &__group {
    display: flex;
    gap: 2px;
    flex-wrap: wrap;
  }

  &__square {
    cursor: pointer;
    height: 10px;
    width: 10px;
  }
}
</style>
