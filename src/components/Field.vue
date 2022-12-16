<script setup>

import { defineProps } from 'vue'

const props = defineProps({
  type: {
    type: String,
    required: true
  },
  name: {
    type: String,
    required: true
  },
  component: {
    type: String,
    required: true
  },
  modelValue: {
    type: [String, Number, Boolean],
    required: true
  }
})

</script>

<template>
  <component
    :is="component"
    :type="props.type !== 'select' ? props.type : undefined"
    :name="props.name"
    :value="modelValue"
    :checked="modelValue"
    @input="$emit('update:modelValue', type == 'checkbox' ? $event.target.checked : $event.target.value)"
  >
    <slot />
  </component>
</template>