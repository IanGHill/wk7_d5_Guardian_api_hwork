<template lang="html">
    <div>
        <li v-on:click="handleClick">
            <h3>{{article.webTitle}}</h3>
            <div class="pad-left">
                <p><b>Section: </b>{{article.sectionName}}  <b>First published: </b>{{formatDates}}  <b>Contributors: </b>{{formatContributors}} </p>
                <!-- <p><b>Section: </b>{{article.sectionName}}</p>
                <p><b>Contributors: </b>{{formatContributors}} </p>
                <p><b>First published: </b>{{formatDates}} </p> -->
            </div>
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
      },
      formatDates: function(){
        return `${this.article.webPublicationDate.substring(8,10)}/${this.article.webPublicationDate.substring(5,7)}/${this.article.webPublicationDate.substring(0,4)}`;
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
    margin: 0.5em; 
  }

  p{
      margin-bottom: 3px;
      margin-top: 3px;
  }
  li{
      list-style-type: none;
      border: #052962 solid 2px;
      margin: 10px;
      padding: 0px 5px 5px 5px;
      background-color: lightgray;
      border-radius: 20px;

  }

  li:hover{
      background-color: silver;
      cursor: pointer;
  }

  .pad-left{
      padding: 0px 10px 0px 10px;
      margin: 0px;
      border: 0px;
  }
</style>