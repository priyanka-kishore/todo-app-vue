<template>
  <h1>TODO with VUE</h1>
  <input type="text" placeholder="What do you got?" id="inputItem" v-model="inputItem" @keyup.enter="addItemToList" />
  <ListCard class="list-card" title="Today" v-model:items="todaysList" />
  <div v-if="errorMessage">{{ errorMessage }}</div>
  <button @click="clearList">Clear Today's List</button>
</template>
<script setup lang="ts">
import { computed, ref } from 'vue';
import ListCard from './components/ListCard.vue';
import { type ListItemProperties } from './components/ListItem.vue';

// data
const inputItem = ref('' as string)
const todaysList = ref([
  { label: 'Walk Theo', isChecked: false },
  { label: 'Go to gym', isChecked: false },
  { label: 'Push code to branch', isChecked: false },
  { label: 'Fix bug', isChecked: false }
] as ListItemProperties[])

// computed properties
const errorMessage = computed(() => {
  if (inputItem.value !== '' && todaysList.value.some(i => i.label === inputItem.value)) {
    return 'You already added this item!'
  }
  return ''
})

// methods
function addItemToList() {
  if (errorMessage.value === '') {
    todaysList.value.push({
      label: inputItem.value,
      isChecked: false
    } as ListItemProperties)

    inputItem.value = '' // clear input
  }
}

function clearList() {
  todaysList.value.splice(0, todaysList.value.length)
}
</script>
<style lang="scss" scoped>
/* adds margin-top to list-cards which have a list-card before it (so on all except first list-card) */
.list-card+.list-card {
  margin-top: 1rem;
}
</style>
