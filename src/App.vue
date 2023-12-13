<template>
  <h1>TODO with Vue</h1>
  <div class="input-group mb-3">
    <input type="text" class="form-control" placeholder="What do you gotta do?" id="inputItem" v-model="inputItem"
      @keyup.enter="addItemToList" />
    <button type="button" class="btn btn-outline-primary" @click="addItemToList" :class="{ disabled : errorMessage }">Add Task</button>
  </div>
  <div class="alert alert-danger" role="alert" v-if="errorMessage">
    {{ errorMessage }}
  </div>
  <ListCard class="list-card" title="Today" v-model:items="todaysList" />
</template>
<script setup lang="ts">
import { computed, onBeforeMount, ref, watch } from 'vue';
import ListCard from './components/ListCard.vue';
import { type ListItemProperties } from './components/ListItem.vue';

// data
const inputItem = ref('' as string)
const todaysList = ref([] as ListItemProperties[])

// computed properties
const errorMessage = computed(() => {
  if (inputItem.value !== '' && todaysList.value.some(i => i.label.toLocaleLowerCase() === inputItem.value.toLocaleLowerCase())) {
    return 'You\'ve already added this item!'
  }
  return ''
})

// lifecycle
onBeforeMount(() => {
  const storedList = localStorage.getItem('list')
  const parsedList = storedList ? JSON.parse(storedList) : []

  todaysList.value.splice(0, todaysList.value.length, ...parsedList)
})

// watchers
watch(todaysList.value, (updatedTodaysList) => {
  localStorage.setItem('list', JSON.stringify(updatedTodaysList as ListItemProperties[]))
}, { deep: true })

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
<style lang="scss" scoped></style>