<template lang="html">
  <div>
    <h1>The Guardian <i>previews</i></h1>
    <section class="main-container">
      <div class="center">
        <article-search :articleSearch='searchString' ></article-search>
      </div>  
    </section>
    <section class="main-container">
        <article-list :articleList='articles' class="flex-item main-left"></article-list>
        <article-detail :articleDetail='articleDetail' class="flex-item main-right"></article-detail>
    </section>
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
      articleDetail: null,
      searchString: ""
    }
  },
  mounted(){
    fetch('https://content.guardianapis.com/search?q=UK%20AND%20news&order-by=newest&page=1&page-size=6&show-tags=contributor&format=json&api-key=6421a937-fac8-4f40-887c-eeddc9bcda34')
    .then(results => results.json())
    // .then(response => this.response = response.response)
    // .then(articles => this.articles = this.response.results)
    .then(articles => this.articles = articles.response.results)
    .then(results => this.selectedArticle = results[0])
    .catch(err => console.log(err))

    eventBus.$on('article-selected', (article) => {
      this.selectedArticle = article
    })

    eventBus.$on('search-entered', (search) => {
      this.searchString = search
    })
    
  },
  watch: {
    selectedArticle: function (oldValue, newValue){
          fetch(`${this.selectedArticle.apiUrl}?show-fields=all&api-key=6421a937-fac8-4f40-887c-eeddc9bcda34`)
          .then(results => results.json())
          .then(articles => this.articleDetail = articles.response.content)
          .catch(err => console.log(err))
    },
        searchString: function (oldValue, newValue){
          fetch(`https://content.guardianapis.com/search?q=${this.searchString}&order-by=newest&page=1&page-size=6&show-tags=contributor&format=json&api-key=6421a937-fac8-4f40-887c-eeddc9bcda34`)
          .then(results => results.json())
          .then(articles => this.articles = articles.response.results)
          .then(results => this.selectedArticle = results[0])
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
    text-align: center;
  }

  h3{
    color: #052962;
    font-family: "Guardian Text Egyptian Web",Georgia,serif;
  }

  .main-container{
    display: flex;
    justify-content: space-between;
    flex: 5;
    flex-direction: row;
  }

  .main-left {
    flex: 4;
    padding: 10px;

  }

  .main-right {
    flex: 1;
    padding: 10px;
  
  }

  .center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  border: 0;
  padding: 0;
}
</style>