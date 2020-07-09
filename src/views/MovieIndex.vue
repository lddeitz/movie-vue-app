<!--
<template>
  <div class="movies-index">

    <h1>{{ message }}</h1>

    <ul>
      <li v-for="error in createErrors">{{ error }}</li>
    </ul>

    <div v-for="movie in movies">
      <p>Title: {{ movie.title }} </p>
      <p>Year: {{ movie.year }} </p>
      <p>Plot: {{ movie.plot }} </p>
      <p>Director: {{ movie.director }} </p>
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
      message: "Check out these movies!"
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
    }
  }
};
</script>
-->

<template>
  <div class="movie-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies">
      <p> Title: {{ movie.title }} </p>
      <p> Plot: {{ movie.plot }} </p>
      <p> Year: {{ movie.year }} </p>
      <p> Director: {{ movie.director }} </p>
      <router-link v-bind:to="`/movies/${movies.id}`">More Info</router-link>
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
    this.indexMovies();
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