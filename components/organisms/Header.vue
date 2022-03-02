<template>
  <nav>
    <div class="left">
      <a class="logo" href="/">News</a>
    </div>
    <div class="right">
      <a class="login" href="/login" v-if="renderLogin()">Login</a>
    </div>
  </nav>
</template>

<script>
  export default {
    methods: {
      renderLogin() {
        return this.$route.path.includes('login')? false : true;
      }
    }
  }
</script>

<style lang="scss">
  nav {
    width: 100vw;
    padding-block: 10px;
    padding-inline: 100px;
    display: flex;
    justify-content: space-between;

    .left {
      display: flex;
      align-items: center;

      .logo {
        font-size: 2rem;
        font-weight: 600;
      }
    }

    .right {
      display: flex;
      align-items: center;
    }

    .login {
      font-size: 16px;
    }
  }

  @media screen and (min-width: 480px) and (max-width: 768px) {
    nav {
      padding-block: 10px;
      padding-inline: 20px;
    }
  }

  @media screen and (max-width: 480px) {
    nav {
      padding-block: 10px;
      padding-inline: 10px;
    }
  }
</style>