<script setup>

import { defineProps, defineEmits, reactive, ref } from 'vue'

const props = defineProps({
  initialValues: {
    type: Object,
    required: true
  },
  validate: {
    type: Function,
    required: true
  },
  onSubmit: {
    type: Function,
    required: true
  },
})

const isSubmitting = ref(false)

const formikStates = reactive({
  values: props.initialValues,
  errors: {},
})

const emits = defineEmits(['submit'])

const handleSubmit = (values) => {
  formikStates.errors = props.validate(values)
  if (!Object.keys(formikStates.errors).length) {
    isSubmitting.value = true
    emits('submit', values, isSubmitting)
  }
}

</script>

<template>
  <slot
    :values="formikStates.values"
    :errors="formikStates.errors"
    :isSubmitting="isSubmitting"
    :handleSubmit="handleSubmit"
  />
</template>