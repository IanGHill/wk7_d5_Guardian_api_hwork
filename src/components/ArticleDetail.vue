<template lang="html">
  <div v-if="articleDetail" class="side-container">
      <h3> {{articleDetail.webTitle}}</h3>
      <h6>{{articleDetail.fields.byline}}</h6>
      <img :src=articleDetail.fields.thumbnail>
      <p>{{articleDetail.fields.bodyText.slice(0,500)}}...</p>
      <!-- <div>{{articleDetail.fields.body}}</div> -->
  </div>
</template>

<script>
export default {
    name: 'article-detail',
    props: ['articleDetail']
}
</script>

<style scoped>
  .side-container{
    float: right;
  }
</style>