<template>
  <input
    type="text"
    :value="value"
    @input="emitUpdates"
    :error="error"
  />
</template>

<script>
  export default {
    props: ['value', 'error'],
    methods: {
      emitUpdates(event) {
        this.$emit("input", event.target.value);
      }
    }
  }
</script>

<style lang="scss">
  input {
    border: 1px solid #E5E0EB;;
    box-sizing: border-box;
    border-radius: 2px;
    padding: 12px;
    font-size: 14px;
  }

  input::placeholder {
    font-size: 14px;
    color: #ABA7AF;
  }

  input:focus {
    outline: none;
  }

  input[error=true] {
    border: 1px solid #D51A52;
  }
</style>