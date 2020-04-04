<template lang="html">
  <div>
    <h1>Guardian News Trawler</h1>
    <div class="main-container">
      <article-list :articleList='articles'></article-list>
      <article-detail :articleDetail='articleDetail'></article-detail>
    </div>  

  </div>
</template>

<script>
import ArticleSearch from './components/ArticleSearch.vue';
import ArticleList from './components/ArticleList.vue';
import ArticleDetail from './components/ArticleDetail.vue';
import { eventBus } from './main.js';

export default {
  name: 'app',
  data (){
    return {
      response: {},
      articles: [],
      selectedArticle: null,
      articleDetail: null
    }
  },
  mounted(){
    fetch('https://content.guardianapis.com/search?q=brexit&page=1&page-size=25&show-tags=contributor&format=json&api-key=6421a937-fac8-4f40-887c-eeddc9bcda34')
    .then(results => results.json())
    // .then(response => this.response = response.response)
    // .then(articles => this.articles = this.response.results)
    .then(articles => this.articles = articles.response.results)
    .catch(err => console.log(err))

    eventBus.$on('article-selected', (article) => {
      this.selectedArticle = article
    })
    
  },
  watch: {
    selectedArticle: function (oldValue, newValue){
          fetch(`${this.selectedArticle.apiUrl}?show-fields=all&api-key=6421a937-fac8-4f40-887c-eeddc9bcda34`)
          .then(results => results.json())
          .then(articles => this.articleDetail = articles.response.content)
          .catch(err => console.log(err))
    }
  },
  components: {
    "article-search": ArticleSearch,
    "article-list": ArticleList,
    "article-detail": ArticleDetail
  }
}
</script>

<style scoped>

  h1{
    color: #052962;
    font-family: "Guardian Text Egyptian Web",Georgia,serif;
  }
  .main-container{
    display: flex;
    justify-content: space-between;
  }
</style>