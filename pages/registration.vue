<template>
  <section>
      <Header />
      <registration-form />
      <Footer />
  </section>
</template>

<script>
  import Header from '../components/organisms/Header.vue'
  import Footer from '../components/organisms/Footer.vue'
  import RegistrationForm from '../components/molecules/RegistrationForm.vue'

  export default {
    components: { RegistrationForm, Header, Footer },
    name: 'RegistrationPage',
  }
</script>

<style>
  /* section {
    height: 100vw;
  } */
</style>