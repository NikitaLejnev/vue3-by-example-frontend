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

    <Field v-slot="{ field, errors }" v-model="startDate" name="startDate">
      <div class="p-col-12">
        <label>Start Date</label>
        <div class="p-inputgroup">
          <Calendar
            inline
            placeholder="Start Date"
            :class="{ 'p-invalid': errors.length > 0 }"
            :minDate="new Date()"
            v-bind="field"
            v-model="startDate"
          />
        </div>
        <InvalidMessage :fieldName="Start date" />
      </div>
    </Field>

    <Field v-slot="{ field, errors }" v-model="endDate" name="endDate">
      <div class="p-col-12">
        <label>End Date</label>
        <div class="p-inputgroup">
          <Calendar
            inline
            placeholder="End Date"
            :class="{ 'p-invalid': errors.length > 0 }"
            v-bind="field"
            v-model="endDate"
            :minDate="new Date(+startDate + 24 * 3600 * 1000)"
          />
        </div>
        <InvalidMessage :fieldName="End date" />
      </div>
    </Field>
  </Form>
</template>
