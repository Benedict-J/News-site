<template>
  <div class="select-container" tabindex="0" @blur="onBlur">
    <div class="select" v-bind="$attrs" @click="handleOpen" :error="error">
      <span class="placeholder" v-if="selected === ''">{{ placeholder }}</span>
      {{ selected }}
    </div>
    <div class="option-list" v-if="open === true">
      <div class="option-item" v-for="(option, i) of options" @focus="onBlur" :key="i" @click="handleOptionClick(option)">
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    inheritAttrs: false,
    props: ['selected', 'options', 'placeholder', 'selected', 'disabled', 'error'],
    data() {
      return {
        open: false,
      }
    },
    methods: {
      emitUpdates() {
        this.$emit("input", this.selectedOption);
      },
      handleOpen() {
        this.disabled !== true? this.open = !this.open : false;
      },
      handleOptionClick(option) {
        this.$emit('update:selected', option);
        this.handleOpen();
      },
      onBlur() {
        this.open = false;
      }
    }
  }
</script>

<style lang="scss">
  .select-container {
    position: relative;

    .select {
      border: 1px solid #E5E0EB;;
      box-sizing: border-box;
      border-radius: 2px;
      box-sizing: border-box;
      padding: 12px;
      font-size: 14px;

      .placeholder {
        color: #ABA7AF;
      }
    }

    .select[error=true] {
      border: 1px solid #D51A52;
    }

    .option-list {
      background-color: white;
      position: absolute;
      left: 0;
      right: 0;
      border-radius: 0px 0px 2px 2px;
      z-index: 1;

      .option-item {
        border: 1px solid #E5E0EB;
        padding: 12px 11px;
        color: #1A141F;
        font-size: 14px;
        font-style: normal;
        font-weight: normal;

        &:hover {
          background: #6C63FF !important;
          color: white;
        }
      }
    }
  }
</style>