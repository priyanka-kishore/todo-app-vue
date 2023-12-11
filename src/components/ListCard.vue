<template>
  <div class="card p-4">
    <div class="card-body">
      <h2 class="card-title">{{ props.title }}</h2>
      <h5 class="card-text mb-4 text-body-tertiary">{{ totalItemsDescription }}</h5>
      <ListItem v-for="item in items" :key="item.label" :item="item" />
    </div>
    <button type="button" class="btn btn-danger mt-3" :class="{ disabled: items.length === 0 }" @click="clearList">Clear Today's List</button>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import ListItem, { type ListItemProperties } from './ListItem.vue'

// props
const props = withDefaults(defineProps<{
  title: string,
  items: ListItemProperties[]
}>(), {})

// data
const items = ref(props.items)

// computed properties
const totalNotChecked = computed(() => items.value.filter(i => !i.isChecked).length)
const totalItemsDescription = computed(() => {
  if (items.value.length === 0) {
    return 'Add some tasks to your list.'
  }

  const itemText = totalNotChecked.value === 1 ? 'task' : 'tasks'
  return totalNotChecked.value === 0
    ? 'You were very productive today!'
    : `You have ${totalNotChecked.value} ${itemText} on your list.`
})

// methods
function clearList() {
  items.value.splice(0, items.value.length)
}
</script>
<style lang="scss" scoped>
</style>