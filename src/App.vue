<template lang="html">
  <div>
    <h1>Guardian News Trawler</h1>
    <div>
      <article-list :articleList='articles'></article-list>
      <article-detail></article-detail>
    </div>  

  </div>
</template>

<script>
import ArticleSearch from './components/ArticleSearch.vue';
import ArticleList from './components/ArticleList.vue';
import ArticleDetail from './components/ArticleDetail.vue';

export default {
  name: 'app',
  data (){
    return {
      response: {},
      articles: [],
      selectedArticle: null
    }
  },
  mounted(){
    fetch('https://content.guardianapis.com/search?q=brexit&page=1&page-size=25&show-tags=contributor&format=json&api-key=test')
    .then(results => results.json())
    // .then(response => this.response = response.response)
    // .then(articles => this.articles = this.response.results)
    .then(articles => this.articles = articles.response.results)
    .catch(err => console.log(err))

    // https://content.guardianapis.com/business/2014/feb/18/uk-inflation-falls-below-bank-england-target?show-fields=all&api-key=test

    
  } ,
  components: {
    "article-search": ArticleSearch,
    "article-list": ArticleList,
    "article-detail": ArticleDetail
  }
}
</script>

<style scoped>

</style>