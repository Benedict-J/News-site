<template>
  <button class="base-button">
    {{ name }}
  </button>
</template>

<script>
  export default {
    props: ['name']
  }
</script>

<style lang="scss">
  button {
    display: flex;
    justify-content: center;
    align-items: center;
    background: #6C63FF;
    border-radius: 4px;
    color: white;
    padding-block: 12px;
    width: 100%;
  }
</style>