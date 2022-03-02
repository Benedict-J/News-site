<template>
  <section>
    <Header />
    <Article />
    <Footer />
  </section>
</template>

<script>
  import Header from '../../components/organisms/Header.vue'
  import Footer from '../../components/organisms/Footer.vue'
  import Article from '../../components/molecules/Article.vue'

  export default {
    components: { Header, Footer, Article },
  }
</script>