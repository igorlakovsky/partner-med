<script setup lang="ts">
export interface ListItemType {
  id: number
  name: string
  count: number
  color: string
  selected: boolean
}

const props = defineProps<{ data: ListItemType }>()
</script>

<template>
  <div class="list-item">
    <input
      type="checkbox"
      :checked="props.data.selected"
      @change="
        () => {
          props.data.selected = !props.data.selected
        }
      "
    />
    <span class="list-item__name">{{ props.data.name }}</span>
    <input
      :value="props.data.count"
      type="number"
      class="list-item__count"
      @change="
        ({ target }) => {
          if (Number((target as HTMLInputElement).value) >= 0 && Number((target as HTMLInputElement).value) <= 100) {
            props.data.count = Math.round(Number((target as HTMLInputElement).value))
          } 
          (target as HTMLInputElement).value = props.data.count as unknown as string
        }
      "
    />
    <input v-model="props.data.color" type="color" class="list-item__color" />
  </div>
</template>

<style lang="scss" scoped>
.list-item {
  display: flex;
  align-items: center;

  &__name {
    margin-left: 6px;
  }

  &__count {
    width: 40px;
    border: none;
    margin-left: auto;

    &:focus-visible {
      outline: none;
    }
  }

  &__color {
    cursor: pointer;
    width: 24px;
    padding: 0px;
    border: 0px;
    background-color: white;
  }
}
</style>
