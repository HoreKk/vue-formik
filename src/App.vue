<script setup>

import FormikVue from './components/Formik.vue';

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
  console.log(values);
  await new Promise((resolve) => setTimeout(resolve, 1000));
  isSubmitting.value = false;
}

</script>

<template>
  <main>
    <FormikVue
      :initialValues="{ email: 'azenoxe@gmail.com' }"
      :validate="validation"
      @submit="handleSubmitTest"
    >
      <template #default="{ values, errors, handleSubmit, isSubmitting }">
        <form @submit.prevent="handleSubmit(values)">
          <input
            type="email"
            name="email"
            v-model="values.email"
          />
          <template v-if="errors.email">
            <p>{{ errors.email }}</p>
          </template>
          <button type="submit" :disabled="isSubmitting">Submit</button>
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
