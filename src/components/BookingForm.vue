<template>
  <Form @submit="onSubmit" :validation-schema="schema">
    <Field v-slot="{ field, errors }" v-model="name" name="name">
      <div class="p-col-12">
        <div class="p-inputgroup">
          <InputText placeholder="Name" :class="{ 'p-invalid': errors.length > 0 }" v-bind="field" />
        </div>
        <small class="p-error" v-if="errors.length > 0">Name is invalid</small>
      </div>
    </Field>
  </Form>
</template>
