<!-- 
This component represents one list and contains multiple ListItem components as to-do items.
Changes to the list here should be reflected up to the parent to update original list (or do two-way binding of list)
-->
<template>
  <div class="card">
    <h1>{{ props.title }}</h1>
    <h2>{{ totalItemsDescription }}</h2>
    <ListItem v-for="item in items" :key="item.label" :label="item.label" v-model:isChecked="item.isChecked"/>
  </div>
</template>

<script setup lang="ts">
import ListItem, { type ListItemProperties } from './ListItem.vue';
import { computed, ref } from 'vue';

// const emit = defineEmits(['update:items']) p

const props = withDefaults(defineProps<{
  title: string,
  items: ListItemProperties[] // the v-model from App.vue parent
}>(), {})

/*  since cannot modify props, need this ref to read items sent via props.
    will not modify props.items. must emit change up to parent. */
const items = ref(props.items)

// TODO need to emit checked status back from ListItem to here to compute this
const totalNotChecked = computed(() => {
  console.log('# undone = ', props.items.filter(i => !i.isChecked).length)
  return props.items.filter(i => !i.isChecked).length
})

const totalItemsDescription = computed(() => {
  if (totalNotChecked.value === 0) {
    return 'You did it all! Awesome work!'
  } else if (totalNotChecked.value === 1) {
    return `${totalNotChecked.value} item`
  } else {
    return `${totalNotChecked.value} items`
  }
})

// function updateItemsList(isChecked: boolean, index: number) {
  // update that item's check
  // items.value[index].isChecked = isChecked
  // emit change up to parent of entire list
  // emit('update:items', items.value)
// }
</script>
<style lang="scss" scoped>
.card {
  border: 2px solid black;
  border-radius: 1rem;
  padding: 2rem;
}
</style>