<script setup lang="ts">
import ListItem, { ListItemType } from './ListItem.vue'

export interface ListProps {
  id: number
  name: String
  items: ListItemType[]
  sorted: boolean
  opened: boolean
}

const props = defineProps<{ lists: ListProps[] }>()

const listIsChecked = (items: ListItemType[]) => {
  return items.every((value) => {
    return value.selected
  })
}

const listIsIndeterm = (items: ListItemType[]) => {
  if (
    items.some((value) => {
      return value.selected
    }) &&
    !items.every((value) => {
      return value.selected
    })
  )
    return true
  return false
}
</script>

<template>
  <section class="nested-list">
    <div v-for="list in props.lists" :key="list.id" class="nested-list__item">
      <img
        :class="{ 'nested-list__arrow': true, 'nested-list__arrow__open': list.opened }"
        src="../assets/arrow.svg"
        @click="
          () => {
            list.opened = !list.opened
          }
        "
      />
      <input
        type="checkbox"
        :checked="listIsChecked(list.items)"
        :indeterminate="listIsIndeterm(list.items)"
        @change="
          ({ target }) => {
            list.items.forEach((item) => {
              item.selected = (target as HTMLInputElement).checked
            })
          }
        "
      />
      <span class="nested-list__name">{{ list.name }}</span>
      <div v-if="list.opened" class="nested-list__childs">
        <ListItem v-for="item in list.items" :key="item.id" :data="item"></ListItem>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.nested-list {
  user-select: none;
  width: fit-content;
  min-width: 340px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding: 20px 10px;
  border: 1px solid #a3a3a3;

  &__item {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
  }

  &__arrow {
    cursor: pointer;
    width: 16px;
    margin-right: 8px;
    transform: rotate(-90deg);
    transition: all 0.1s;

    &__open {
      transform: rotate(0deg);
    }
  }

  &__name {
    padding-left: 6px;
  }

  &__childs {
    width: 100%;
    margin: 0px 50px;
    display: flex;
    flex-direction: column;
    margin-top: 6px;
  }
}
</style>
