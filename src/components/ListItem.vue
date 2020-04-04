<template lang="html">
    <div>
        <li v-on:click="handleClick">
            <h3>{{article.webTitle}}</h3>
            <h4>Section: {{article.sectionName}}</h4>
            <span><b>First published: </b>{{article.webPublicationDate.substring(8,10)}}/{{article.webPublicationDate.substring(5,7)}}/{{article.webPublicationDate.substring(0,4)}} </span><br><br>
            <span><b>Contributors: </b></span><span >{{formatContributors}} </span><br>
        </li>
    </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
    name: "list-item",
    props: ['article'],
    computed: {
      formatContributors: function(){
       switch (this.article.tags.length){
            case 0:
               return 'None listed';
            case 1:
                return this.article.tags[0].webTitle;
            default:
                var authorString = "";
                this.article.tags.forEach(element => {
                    authorString = authorString.concat(element.webTitle , ', ');
                });
                authorString = authorString.substring(0, (authorString.length - 2))
                return authorString;
       }
      }
    },
    methods: {
        handleClick(){
            eventBus.$emit('article-selected', this.article)
        }
    }
}
</script>

<style scoped>
  h3{
    color: #052962;
    font-family: "Guardian Text Egyptian Web",Georgia,serif;
  }

  li{
      list-style-type: none;
      border: #052962 solid 2px;
      margin: 10px;
      padding: 5px;
      background-color: silver;
      border-radius: 20px;

  }
</style>