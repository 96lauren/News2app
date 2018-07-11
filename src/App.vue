<template>
  <div class="container">
    <div v-for="article in news">
  <img :src="article.urlToImage" alt="">
  
      <h3>{{article.title}}</h3>
  
      <h4>{{article.author}}</h4>
      
      <p> {{article.description}}</p>
      <a class="button" :href= "article.url" target="_blank" >read more</a>

  </div>
  </div>
</template>

<script>

import axios from 'axios'

const url = "https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=49bc9bb4ad4b41fc93bdea885a96c962";
const data = {
news:[ ]
   
}

export default {
  data: function() { 
    return data

  },

  created() {
  	this.loadNews();
  },

  methods:{
  	loadNews(){
      axios.get(url).then(function(response) {
 	    console.log(response.data.articles)
          data.news= response.data.articles
  
  }).catch(function(error){
  		  console.log(error.message)
  
  })
  
  
  }
  }
}
</script>
