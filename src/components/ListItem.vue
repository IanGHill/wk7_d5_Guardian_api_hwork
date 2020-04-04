<template lang="html">
    <div>
        <li v-on:click="handleClick">
            <h3>{{article.webTitle}}</h3>
            <h4>Section: {{article.sectionName}}</h4>
            <span>Contributors: </span><span v-for="(tag, index) in article.tags" :key="index">{{tag.webTitle}} </span>
        </li>
    </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
    name: "list-item",
    props: ['article'],
    methods: {
        handleClick(){
            eventBus.$emit('article-selected', this.article)
        }
    }
}
</script>

<style scoped>

</style>