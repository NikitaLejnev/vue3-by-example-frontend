<template>
  <Form @submit="onSubmit" :validation-schema="schema">
    <Field v-slot="{ field, errors }" v-model="name" name="name">
      <div class="p-col-12">
        <div class="p-inputgroup">
          <InputText placeholder="Name" :class="{ 'p-invalid': errors.length > 0 }" v-bind="field" />
        </div>
        <InvalidMessage :fieldName="Name" />
      </div>
    </Field>

    <Field v-slot="{ field, errors }" v-model="address" name="address">
      <div class="p-col-12">
        <div class="p-inputgroup">
          <InputText
            placeholder="Address"
            :class="{ 'p-invalid': errors.length > 0 }"
            v-bind="field"
          />
        </div>
        <InvalidMessage :fieldName="Address" />
      </div>
    </Field>
  </Form>
</template>
