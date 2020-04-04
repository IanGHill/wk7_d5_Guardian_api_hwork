<template lang="html">
  <div>
      <ul>
          <list-item v-for="(article, index) in articleList" :article="article" :key="index"></list-item>
      </ul>
  </div>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
    name: 'article-list',
    props: ['articleList'],
    components: {
        "list-item": ListItem
    }
}
</script>

<style scoped>

</style>