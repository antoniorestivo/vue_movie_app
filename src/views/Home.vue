<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>New Movie</h2>
    <div>
    Title: <input type="text" v-model="newTitle" /> <br />
      Year: <input type="number" v-model="newYear" /><br />
      Plot: <input type="text" v-model="newPlot" /><br />
      Director: <input type="text" v-model="newDirector" /><br />
      English: <input type="checkbox" v-model="newEnglish" /><br />
      <button v-on:click="createMovie()">Create</button>
      </div>
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
      newTitle: "",
      newYear: 0,
      newPlot: "",
      newDirector: "",
      newEnglish: true
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function(){
     axios.get("/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
       });
   },
    createMovie: function(){
    var params = {
        
         title: this.newTitle,
         year: this.newYear,
         plot: this.newPlot,
         director: this.newDirector,
         english: this.newEnglish

       };
       axios
      .post("/api/movies", params)
      .then((response) => {
          console.log(response.data);
           this.movies.push(response.data);
         })
         .catch((error) => {
            console.log(error.response.data.errors);
          });
    }
   
  },
};
</script>




