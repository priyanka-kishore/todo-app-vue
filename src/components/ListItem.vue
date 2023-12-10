<template>
  <div>
    <input type="checkbox" :id="item.label" v-model="item.isChecked" />
    <label :for="item.label" :class="{ checked: item.isChecked }">{{ item.label }}</label>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// setup
export type ListItemProperties = {
  label: string
  isChecked: boolean
}

// props
const props = withDefaults(defineProps<{
  item: ListItemProperties
}>(), {})

// data
const item = ref(props.item) // reactive version of props.item
</script>

<style lang="scss" scoped>
label {
  margin-left: 1rem;
}

.checked {
  text-decoration: line-through;
}
</style>