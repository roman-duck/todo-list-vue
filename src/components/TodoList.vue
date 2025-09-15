<script lang="ts" setup>
import { ref } from 'vue'
import type { Ref } from 'vue'
import ListItem from './ListItem.vue'

type Item = {
  title: string
  checked?: boolean
}

const ListItems: Ref<Item[]> = ref([
  { title: 'make a todo list app', checked: true },
  { title: 'Predict the weather', checked: false },
  { title: 'Play some tunes', checked: false },
  { title: 'Pump some iron', checked: false },
  { title: 'Track my expences', checked: false },
  { title: 'Learn a new language', checked: false },
  { title: 'Publish my work', checked: false },
])

const updateItem = (item: Item): void => {
  const updatedItem = findItemInList(item)
  if (updatedItem) {
    toggleItemChecked(updatedItem)
  }
}

const findItemInList = (item: Item): Item | undefined => {
  return ListItems.value.find((itemInList: Item) => itemInList.title === item.title)
}

const toggleItemChecked = (item: Item): void => {
  item.checked = !item.checked
}
</script>

<template>
  <ul>
    <li :key="key" v-for="(item, key) in ListItems">
      <ListItem :isChecked="item.checked" v-on:click.prevent="updateItem(item)">{{
        item.title
      }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
}

li {
  margin: 0.4rem 0;
}
</style>
