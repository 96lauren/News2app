<template>
  
  <div class="container">
  	<h1>Top trending news WorldWide </h1>
    <div v-for="article in news">
  <img :src="article.urlToImage" alt="">
  
      <h3><strong>{{article.title}}</strong></h3>
  
      <h4>{{article.author}}</h4>
      
      <p> {{article.description}}</p>
      <a class="button" :href= "article.url" target="_blank" >read more</a>
      <hr>

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
