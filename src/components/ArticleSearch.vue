<template lang="html">
  <div>
    <form v-on:submit.prevent="handleSearch">
        <label for="search_box">Search Guardian website: </label>
        <input type="text" id="search_box" v-model="searchString"/>
        <input type="submit" value ="Search" />
    </form>
  </div>
</template>

<script>

import { eventBus } from '../main.js';

export default {
    name: 'article-search',
    data(){
        return{
            searchString: ""
        }
    },
    props: ['articleSearch'],
    methods: {
        handleSearch(){
            eventBus.$emit('search-entered', this.searchString)
            this.searchString = ""
        }
    }

}
</script>

<style scoped>

</style>