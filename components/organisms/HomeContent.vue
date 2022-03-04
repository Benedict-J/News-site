<template>
  <div class="home">
    <h1>Lastest News</h1>
    <div class="article-list">
      <div class="article-container" v-for="(article, i) of articles.articles" :key="i" @click="() => redirectToArticle(article)">
        <img :src="article.urlToImage" v-if="article.urlToImage !== 'null'" />
        <div>
          <div class="article-time">{{ getDateTime(article.publishedAt) }}</div>
          <div class="article-title">{{ article.title }}</div>
          <div class="article-desc">{{ article.description }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import BaseButton from '../atoms/BaseButton.vue';

  export default {
  components: { BaseButton },
    data() {
      return {
        articles: []
      }
    },
    methods: {
      async asyncData() {
        console.log(process.env.NEWSAPI)
        this.articles = await fetch(`/api/everything?sources=business-insider&sortBy=publishedAt`, {
            headers: { 
              'Authorization': 'Bearer ' + process.env.NEWS_API
              }
          }).then(res => {
            return res.json();
          });
      },
      getDateTime(value) {
        let date = new Date(value);
        return date.toLocaleString("en-us", { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' });
      },
      redirectToArticle(article) {
        let uid = new Date(article.publishedAt).toString(36) + Math.random().toString(36).substring(2);
        localStorage.setItem('article', JSON.stringify(article));
        this.$router.push(`/article/${uid}`);
      }
    },
    mounted() {
      this.asyncData();
    }
  }
</script>

<style lang="scss">
  .home {
    display: flex;
    margin-inline: 100px;
    margin-block: 50px;
    flex-direction: column;

    h1 {
      font-style: normal;
      font-weight: 500;
      font-size: 40px;
      margin-bottom: 20px;
    }

    .article-list {
      display: flex;
      flex-wrap: wrap;
      row-gap: 50px;
      column-gap:  100px;

      .article-container {
        width: 350px;

        img {
          border-radius: 5px;
        }

        .article-time {
          margin-top: 5px;
          font-weight: 300;
          font-size: 14px;
        }

        .article-title {
          display: flex;
          flex-direction: column;
          font-size: 24px;
          font-style: normal;
          font-weight: 600;
          margin-bottom: 5px;
        }

        .article-desc {
          font-size: 14px;
        }
      } 
    }
  }

  @media screen and (min-width: 769px) and (max-width: 1024px) {
    .home {
      .article-list {
        .article-container {
          width: 100%;
        }
      }
    }
  }

  @media screen and (min-width: 480px) and (max-width: 768px) {
    .home {
      .article-list {
        .article-container {
          width: 100%;
        }
      }
    }
  }

  @media screen and (max-width: 480px) {
    .home {
      margin: 0;
      flex-direction: column;
      align-items: center;

      .article-list {
        flex-direction: column;
        flex-wrap: nowrap;

        .article-container {
          max-width: 350px;

          .article-title {
            font-size: 18px;
          }
        }
      }
    }
  }
</style>