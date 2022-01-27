<template>
  <small class="p-error" v-if="errors.length > 0">{{ fieldName }} is invalid</small>
</template>

<script>
export default {
  name: "InvalidMessage",
  props: {
    fieldName: String
  },
}
</script>
