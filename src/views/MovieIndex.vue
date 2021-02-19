<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div>Search by title: <input v-model="titleFilter">
    Search by name: <input v-model="titleFilter" list="titles">
<datalist id="titles">
	<option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
</datalist>
    <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">

      
      <h2>Movie Title: {{movie.title}}</h2>
      <h3>Movie Year: {{movie.year}}</h3>
      <h4>Movie Plot: {{movie.plot}}</h4>
      <h5>Movie Director: {{movie.director}}</h5>
      <h6>Movie in English:{{movie.english}}</h6>

  </div>
  </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Movie List",
      movies:[],
      titleFilter: "",

      
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