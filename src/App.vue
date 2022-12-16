<script setup>

import FormikVue from './components/Formik.vue';
import Field from './components/Field.vue';

import { ref } from 'vue';

const submitValues = ref({});

const validation = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = 'Required';
  } else if (
    !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
  ) {
    errors.email = 'Invalid email address';
  }
  return errors;
}

const handleSubmitTest = async (values, isSubmitting) => {
  submitValues.value = JSON.parse(JSON.stringify(values));
  isSubmitting.value = false;
}

</script>

<template>
  <main>
    <FormikVue
      :initialValues="{ email: '', isStaff: false, date: '', select: '' }"
      :validate="validation"
      @submit="handleSubmitTest"
    >
      <template #default="{ values, errors, handleSubmit, isSubmitting }">
        <form
          style="display: flex; flex-direction: column; gap: 10px; align-items: flex-start;"
          @submit.prevent="handleSubmit(values)"
        >
          <h1>Formik in Vue</h1>
          <Field
            type="email"
            name="email"
            component="input"
            v-model="values.email"
          />
          <template v-if="errors.email">
            <p>Email : {{ errors.email }}</p>
          </template>
          <Field
            type="checkbox"
            name="isStaff"
            component="input"
            v-model="values.isStaff"
          />
          <template v-if="errors.isStaff">
            <p>IsStaff : {{ errors.isStaff }}</p>
          </template>
          <Field
            type="date"
            name="date"
            component="input"
            v-model="values.date"
          />
          <template v-if="errors.date">
            <p>Date : {{ errors.date }}</p>
          </template>
          <Field
            type="select"
            name="select"
            component="select"
            v-model="values.select"
          >
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
          </Field>
          <template v-if="errors.select">
            <p>Select : {{ errors.select }}</p>
          </template>
          <div>
            {{ JSON.stringify(submitValues, null, 4) }}
          </div>
          <button type="submit" :disabled="isSubmitting">
            Submit
          </button>
        </form>
      </template>
    </FormikVue>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
