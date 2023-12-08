<template>
  <div>
    <input type="checkbox" :id="props.label" v-model="isChecked" @input="$emit('update:isChecked', isChecked)">
    <label :for="props.label" :class="{ checked: isChecked }">{{ props.label }}</label>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

export type ListItemProperties = {
  label: string
  isChecked: boolean
}

defineEmits(['update:isChecked'])

const props = withDefaults(defineProps<{
  label: string,
  isChecked: boolean // changes must be emitted to parent
}>(), {
  isChecked: false as boolean
})

/*  since cannot modify props, need this ref to read if item checked or not. 
    will not modify props.isChecked. must emit change up to parent. */
const isChecked = ref(props.isChecked) 

// const item = ref(props.item)
</script>

<style lang="scss" scoped>
label {
  margin-left: 1rem;
}

.checked {
  text-decoration: line-through;
}
</style>