<template>
  <div class="article">
    <div class="article-content">
      <div class="title-container">
        <h1 class="article-title">{{ article.title }}</h1>
      </div>
      <div class="article-details">
        <span class="article-time">Source: Business Insider - {{ getDateTime(article.publishedAt) }}</span>
        <span class="article-author">Author: {{ article.author }}</span>
      </div>
      <img class="article-mainImg" :src="article.urlToImage" />
      <p>
        {{ article.content }}
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        article: {},
      }
    },
    methods: {
      readArticle() {
        this.article = JSON.parse(localStorage.getItem('article'));
      },
      getDateTime(value) {
        let date = new Date(value);
        return date.toLocaleString("en-us", { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit' });
      },
    },
    mounted() {
      this.readArticle();
    }
  }
</script>

<style lang="scss">
  .article {
    margin-block: 50px;
    display: flex;
    justify-content: center;

    .article-content {
      width: 60vw;

      .article-title {
        font-size: 28px;
        font-weight: 500;
      }

      .article-details {
        display: flex;
        flex-direction: column;
        margin-block: 10px;

        .article-time {
          font-weight: 300;
          font-size: 14px;
        }

        .article-author {
          font-weight: 300;
          font-size: 14px;
        }
      }

      img {
        max-height: 400px;
      }

      p {
        margin-block: 20px;
      }
    }
  }

  @media screen and (max-width: 1024px) {
    .article {
      .article-content {
        width: 90vw;

        .article-title {
          font-size: 20px;
          font-weight: 600;
        }

        .article-details {
          .article-time {
            font-weight: 300;
            font-size: 12px;
          }

          .article-author {
            font-weight: 300;
            font-size: 12px;
          }
        }

        .article-mainImg {
          width: 100%;
          height: initial;
        }

        p {
          font-size: 14px;
        }
      }
    }
  }
</style>