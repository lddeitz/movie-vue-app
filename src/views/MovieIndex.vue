<template>
  <div class="movie-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies">
      <p> Title: {{ movie.title }} </p>
      <p> Plot: {{ movie.plot }} </p>
      <p> Year: {{ movie.year }} </p>
      <p> Director: {{ movie.director }} </p>
      <router-link v-bind:to="`/movies/${movie.id}`">More Info</router-link>
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
      message: "Check out these movies!",
      movies: []
    };
  },
  created: function() {
    // this.indexMovies();
    axios.get("/api/movies").then(response => {
      console.log("All Movies:", response.data);
      this.movies = response.data;
    });
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("All Movies:", response.data);
        this.movies = response.data;
      });
    }
  }
};
</script>