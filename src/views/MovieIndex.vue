<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Movie Title: {{movie.title}}</h2>
      <h3>Movie Year: {{movie.year}}</h3>
      <h4>Movie Plot: {{movie.plot}}</h4>
      <h5>Movie Director: {{movie.director}}</h5>
      <h6>Movie in English:{{movie.english}}</h6>

  </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Movie List",
      movies:[],
      
    };
  },
  created: function() {
        axios.get("/api/movies").then(response => {
        console.log(response.data);
        this.movies = response.data;
       });
  },
  methods: {
   
  },
    
   
  };
</script>