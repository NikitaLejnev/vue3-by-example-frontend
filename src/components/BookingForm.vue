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

    <div class="p-col-12">
      <Button label="Book" type="submit" />
    </div>
  </Form>
</template>

<script>
import { Form, Field } from "vee-validate";
import * as yup from "yup";
import axios from "axios";
import { InvalidMessage } from "./InvalidMessage.vue";
import { APIURL } from "@/constants";

const schema = yup.object().shape({
  name: yup.string().required(),
  address: yup.string().required(),
  startDate: yup.date().required(),
  endDate: yup
    .date()
    .required()
    .when("startDate",
      (startDate, schema) => startDate &&
        schema.min(startDate)
    ),
});

export default {
  name: "BookingForm",
  components: {
    Form,
    Field,
    InvalidMessage,
  },
  props: {
    selectedCatalogId: Number,
  },
  data() {
    return {
      name: "",
      address: "",
      startDate: undefined,
      endDate: undefined,
      schema,
    };
  },
  methods: {
    async onSubmit(values) {
      const { name, address, startDate, endDate } = values;
      await axios.post(`${APIURL}/bookings`, {
        name,
        address,
        startDate,
        endDate,
        catalogItemId: this.selectedCatalogId,
      });
      this.$emit("booking-form-close");
    },
  },
};
</script>
