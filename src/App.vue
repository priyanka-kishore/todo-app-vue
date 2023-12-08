<template>
  <h1>TODO with VUE</h1>
  <input type="text" placeholder="What you got?" id="inputItem" v-model="inputItem" @keyup.enter="addToList" />
  <ListCard class="list-card" title="Today" v-model:items="todaysList" />
  <div>{{ errorMessage }}</div>
  <button @click="deleteAllItems">Delete All Tasks</button>
  <div>{{ todaysList }}</div>
</template>
<script setup lang="ts">
import { computed, ref } from 'vue';
import ListCard from './components/ListCard.vue';
import { type ListItemProperties } from './components/ListItem.vue';

const inputItem = ref('' as string)
const todaysList = ref([
  { label: 'Walk Theo', isChecked: false },
  { label: 'Go to gym', isChecked: false },
  { label: 'Push code to branch', isChecked: false },
  { label: 'Fix bug', isChecked: false }
] as ListItemProperties[])

const errorMessage = computed(() => {
  if (inputItem.value !== '' && todaysList.value.some(i => i.label === inputItem.value)) {
    return 'You already added this item!'
  }
  return ''
})

function addToList() {
  if (errorMessage.value === '') {
    todaysList.value.push({
      label: inputItem.value,
      isChecked: false
    } as ListItemProperties)

    // clear input
    inputItem.value = ''
  }
}

function deleteAllItems() {
  todaysList.value.splice(0, todaysList.value.length)
}
</script>
<style lang="scss" scoped>
/* adds margin-top to list-cards which have a list-card before it (so on all except first list-card) */
.list-card+.list-card {
  margin-top: 1rem;
}
</style>
