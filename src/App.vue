<template>
  <h1>TODO with Vue</h1>
  <div class="input-group mb-3">
    <input type="text" class="form-control" placeholder="What do you gotta do?" id="inputItem" v-model="inputItem" @keyup.enter="addItemToList" />
    <button type="button" class="btn btn-outline-primary" @click="addItemToList">Add Task</button>
  </div>
  <ListCard class="list-card" title="Today" v-model:items="todaysList" />
  <div v-if="errorMessage">{{ errorMessage }}</div>
</template>
<script setup lang="ts">
import { computed, ref } from 'vue'
import ListCard from './components/ListCard.vue'
import { type ListItemProperties } from './components/ListItem.vue'

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
</script>
<style lang="scss" scoped>
</style>
