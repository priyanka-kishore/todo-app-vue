<template>
  <ul class="list-group">
    <li class="list-group-item border-0 py-1">
      <input class="form-check-input me-1" type="checkbox" :id="item.label" v-model="item.isChecked" />
      <label class="form-check-label" :for="item.label" :class="{ checked: item.isChecked }">{{ item.label }}</label>
    </li>
  </ul>
</template>

<script setup lang="ts">
import { ref } from 'vue'

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
  margin-left: 1rem
}

.checked {
  text-decoration: line-through
}
</style>