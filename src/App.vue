<template>
  
  <div class="container">
  	<h1>Top trending news WorldWide </h1>
    <input v-model="search" type="search " name="search" placeholder=" type to search">
    <br>
    <button v-on:click="loadNews" type="button">search</button>
    <p  v-if="loading"> please wait...</p>
    
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
const baseurl ="https://newsapi.org/v2";
const apikey ="49bc9bb4ad4b41fc93bdea885a96c962";
const endpoint="/everything";

const data = {
news:[ ],
search:'',
loading:false 
   
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
      if(this.search.length<1){
        return;
      }
      this.loading= true;

      this.news =[ ];

      let url = baseurl + endpoint + '?q=' +this.search + '&apikey='+apikey;

      axios.get(url).then(function(response) {
 	    console.log(response.data.articles)
      data.loading = false;
      data.news= response.data.articles
  
  }).catch(function(error){
  		  console.log(error.message)
  
  })
  
  
  }
  }
}
</script>
