<template>
  <section>
      <Header />
      <LoginForm />
      <Footer />
  </section>
</template>

<script>
  import Header from '../components/organisms/Header.vue'
  import Footer from '../components/organisms/Footer.vue'
  import LoginForm from '../components/molecules/LoginForm.vue'

  export default {
    components: { Header, Footer, LoginForm },
    name: 'LoginPage',
  }
</script>