<template>
  <label>{{ label }}<span class="required" v-if="required">*</span></label>
</template>

<script>
  export default {
    props: {
      label: {
        type: String,
        required: true,
      },
      required: {
        type: String
      }
    },
  }
</script>

<style lang="scss">
  label {
    font-size: 16px;
    font-weight: normal;
    font-style: normal;
    margin-bottom: 4px;

    .required {
      color: red;
    }
  }
</style>