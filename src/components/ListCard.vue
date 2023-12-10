<template>
  <div class="card">
    <h1>{{ props.title }}</h1>
    <h2>{{ totalItemsDescription }}</h2>
    <ListItem v-for="item in props.items" :key="item.label" :item="item" />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import ListItem, { type ListItemProperties } from './ListItem.vue';

// props
const props = withDefaults(defineProps<{
  title: string,
  items: ListItemProperties[]
}>(), {})

// computed properties
const totalNotChecked = computed(() => props.items.filter(i => !i.isChecked).length)
const totalItemsDescription = computed(() => {
  const itemText = totalNotChecked.value === 1 ? 'item' : 'items';
  return totalNotChecked.value === 0
    ? 'Look how productive you were today!'
    : `${totalNotChecked.value} ${itemText}`;
})
</script>
<style lang="scss" scoped>
.card {
  border: 2px solid black;
  border-radius: 1rem;
  padding: 2rem;
}
</style>