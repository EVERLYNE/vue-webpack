<template>
  <div class="container">

  <input v-model ='search' type="search" name="search"value="" placeholder="Type to search...">
            <button v-on:click="loadNews"type="button">search</button>
            <p v-if="loading"> please wait....</p>
            <div class="lds-roller"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
            
       
  

<div class="content" v-for = "article in news">

<img v-if="article.urlToImage":src="article.urlToImage" alt="">



<h3>
  {{article.title}}
</h3>
<h4>{{article.author}}</h4>

<p>{{article.description}}</p>
<blockquote>
<a href="#"target="_blank" class="button">Read more</a>
</blockquote>




</div>


   
    

  </div>

</template>

<script>
 const baseurl="https://newsapi.org/v2";
 const apiKey="0704dbd41e354875bb6e070684ab2f39";
 const endpoint="/everything";

 


import axios from 'axios'

const data = {
  news:[],
  search:'',
  loading:false
  
  
  
}


export default {
  data: function() {
    return data
  },
  created(){
 this.loadNews()
  },
  methods:{
    loadNews() {
      if(this.search.length<1){
        return
      }
      this.loading =true;
      this.news =[];
      let  url = baseurl + endpoint +'?q=' + this.search + '&apikey=' +apiKey;
 axios.get(url).then(function(response) {
    console.log(response.data.articles)
    data.loading = false;
    data.news = response.data.articles
  }).catch(function(error){
  console.log(error.message)
  })
  
  }
  }
}
</script>


