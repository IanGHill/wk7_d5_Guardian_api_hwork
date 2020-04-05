<template lang="html">
  <div class="main-container">
    <form v-on:submit.prevent="handleSearch" >
        <label for="search_box" class="form-inline">Search: </label>
        <input type="text" id="search_box" v-model="searchString" />
        <label for="search_priority" >Order by: </label>
        <select id="search_priority" v-model="searchPriority" >
            <option value="newest" selected="selected">Most Recent</option>
            <option value="relevance">Most Relevant</option>
        </select>
        <input type="submit" value ="Search" class="button"/>
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
            var newSearchString = this.searchString.replace(/ /g, "%20AND%20")
            eventBus.$emit('search-entered', newSearchString)
            this.searchString = ""
            
            eventBus.$emit('search-priority', this.searchPriority)
            this.searchPriority = ""
        }
    }

}
</script>

<style scoped>

input {
  vertical-align: middle;
  margin: 0px 20px 0px 10px;
  padding: 10px;
  background-color: #f8f8f8;
  border: 1px solid #aaa;
  box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
  color: #444;
  font-size: 16px;
  font-family: sans-serif;
  font-weight: 300;
}

label{
    color: #052962;
    font-size: 1.2em;
    font-weight: bold;
    vertical-align: middle;
}

.button {
  vertical-align: middle;
  padding: 10px 20px;
  border: 1px solid #052962;
  color: black;
  margin: 0px 20px 0px 10px;
  font-size: 1em;

}

.button:hover {
  background-color: #052962;
  color: white;
  cursor: pointer;
}

select {
    vertical-align: middle;
	font-size: 16px;
	font-family: sans-serif;
	font-weight: 300;
	color: #444;
	padding: 10px;
	margin: 0px 20px 0px 10px;
	border: 1px solid #aaa;
	box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
	border-radius: .2em;
	appearance: none;
}
select:hover {
    cursor: pointer;
}

</style>