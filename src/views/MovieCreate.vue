<template>
<div class="movie-create">
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
</div>
</template>

<script>
import axios from "axios";
export default {
  data: function(){
    return {
     newTitle: "",
     newYear: 0,
     newPlot: "",
     newDirector: "",
     newEnglish: true,
    };
  },
  created: function() {},
  methods: {
    createMovie: function() {
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

    },
  },
};
</script>