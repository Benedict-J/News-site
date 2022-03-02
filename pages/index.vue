<template>
  <section>
      <Header />
      <HomeContent />
      <Footer />
  </section>
</template>

<script>
  import Header from '../components/organisms/Header.vue'
  import Footer from '../components/organisms/Footer.vue'
  import HomeContent from '../components/organisms/HomeContent.vue'

  export default {
    components: { Header, Footer, HomeContent },
    name: 'HomePage',
  }
</script>