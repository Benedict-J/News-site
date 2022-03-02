<template>
  <div class="login-form">
    <div class="left">
      <div class="title">
        <h1>Login</h1>
      </div>
      <form @submit.prevent="handleSubmit" novalidate>
        <div class="error">
          {{ error.message }}
        </div>
        <div class="form-input">
          <base-label label="Email" />
          <base-input placeholder="Email" v-model="input.email" />
        </div>
        <div class="form-input">
          <base-label label="Password" />
          <base-input placeholder="********" type="password" v-model="input.password" />
        </div>
        <div class="button-container">
          <base-button name="Submit" />
        </div>
        <span>Don't have an account? <a href="/registration" class="register-link">Sign up</a></span>
      </form>
    </div>
    <div class="right">
      <img src="../../assets/images/undraw_Login_re_4vu2.png" />  
    </div>
  </div>
</template>

<script>
  import BaseLabel from '../atoms/BaseLabel.vue'
  import BaseInput from '../atoms/BaseInput.vue'
  import BaseButton from '../atoms/BaseButton.vue'

  export default {
    components: { BaseInput, BaseLabel, BaseButton },
    data() {
      return {
        input: {
          email: '',
          password: ''
        },
        error: {
          message: ''
        },
      };
    },
    methods: {
      handleSubmit() {
        this.$router.push("/");
      }
    }
  }
</script>

<style lang="scss">
  .login-form {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    margin-block: 100px;

    .left {
      display: flex;
      flex-direction: column;
      width: 280px;
    }

    .title {
      margin-bottom: 15px;

      h1 {
        font-style: normal;
        font-weight: 500;
        font-size: 30px;
      }
    }

    form {
      display: flex;
      flex-direction: column;
      row-gap: 10px;
      z-index: 0;

      .form-input-group {
        display: flex;
        justify-content: space-between;
        column-gap: 20px;
      }

      .form-input {
        display: flex;
        flex-direction: column;
      }

      .button-container {
        width: 100%;
        margin-top: 20px;
      }

      .register-link {
        color: #6C63FF;
      }
    }

    .right {
      display: flex;
      align-items: center;
      width: 40vw;
    }
  }

  @media screen and (max-width: 1024px) {
    .login-form {
      margin-block: 60px;

      .title {
        width: 100%;
        display: flex;
      }

      form {
        width: 100%;

        .form-input-group {
          display: flex;
          flex-direction: column;
          row-gap: 10px;
        }
      }

      .right {
        display: none;
      }
    }
  } 
</style>