<template lang="html">
  <div v-if="articleDetail" class="article-box">
      <h3> <a :href=articleDetail.webUrl target="_blank" rel="noreferrer noopener">{{articleDetail.webTitle}}</a></h3>
      <h4>{{articleDetail.fields.byline}}</h4>
      <img :src=articleDetail.fields.thumbnail>
      <p>{{articleDetail.fields.bodyText.slice(0,1000)}}...</p>
      <p><b>Continue to full article on <a :href=articleDetail.webUrl target="_blank" rel="noreferrer noopener">The Guardian website</a></b></p>
  </div>
</template>

<script>
export default {
    name: 'article-detail',
    props: ['articleDetail']
}
</script>

<style scoped>
  h3{
    color: #052962;
    font-family: "Guardian Text Egyptian Web",Georgia,serif;
  }

.article-box{
      list-style-type: none;
      border: #052962 solid 2px;
      margin: 30px;
      padding: 5px;
      border-radius: 20px;

  }
</style>