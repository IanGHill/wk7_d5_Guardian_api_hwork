<template lang="html">
  <div>
    <form v-on:submit.prevent="handleSearch">
        <label for="search_box">Search The Guardian website: </label>
        <input type="text" id="search_box" v-model="searchString"/>
        <label for="search_priority">Search priority: </label>
        <select id="search_priority" v-model="searchPriority">
            <option value="newest" selected="selected">Newest</option>
            <option value="relevance">Relevance</option>
        </select>
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
            searchString: "",
            searchPriority: ""
        }
    },
    props: ['articleSearch'],
    methods: {
        handleSearch(){
            eventBus.$emit('search-entered', this.searchString)
            this.searchString = ""
            
            eventBus.$emit('search-priority', this.searchPriority)
            this.searchPriority = ""
        }
    }

}
</script>

<style scoped>

</style>