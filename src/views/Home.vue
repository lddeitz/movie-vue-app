<template>
  <div class="home">

    <h1>{{ message }}</h1>
    <button v-on:click="indexMovies()">Show Movies</button>

    <ul>
      <li v-for="error in createErrors">{{ error }}</li>
    </ul>

    <div v-for="movie in movies">
      <p>Title: {{ movie.title }} </p>
      <p>Year: {{ movie.year }} </p>
      <p>Plot: {{ movie.plot }} </p>
      <p>Director: {{ movie.director }} </p>
        <button v-on:click="updateMovie(currentMovie)">Show More</button>
      <br>
      <br>
    </div>

    <dialog id="movie details">
      <form method="dialog">
        <h2> Movie Info </h2>
        <p>Title: <input type="text" v-model="currentMovie.Title"></p>
        <p>Year: <input type="text" v-model="currentMovie.Year"></p>
        <p>Plot: <input type="text" v-model="currentMovie.Plot"></p>
        <p>Director: <input type="text" v-model="currentMovie.Director"></p>
        <button v-on:click="destroyMovie(currentMovie)">Delete</button>
        <button v-on:click="updateMovie(currentMovie)">Edit</button>
        <button>Close</button>
      </form>
    </dialog>

    <div>
      Title: <input type="text" v-model="newMovieTitle"> <br>
      Year: <input type="text" v-model="newMovieYear"> <br>
      Plot: <input type="text" v-model="newMoviePlot"> <br>
      Director: <input type="text" v-model="newMovieDirector"> <br>
      <button v-on:click="createMovie()">Create</button> <br>
    </div>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
      createErrors: [],
      message: "Welcome to Vue.js!",
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      currentMovie: {}
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("All Movies:", response.data);
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          console.log("Success", response.data);
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.createErrors = error.response.data.errors;
        });
    },
    showMovie: function(movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director
      };
      axios
        .patch(`api/movies/${movie.id}`, params)
        .then(response => {
          console.log("Successfully updated", response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
          // this.createErrors = error.response.data.errors;
        });
    },
    destroyMovie: function(movie) {
      axios.delete(`api/movies/${movie.id}`).then(response => {
        console.log("Successfully destroyed", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>
