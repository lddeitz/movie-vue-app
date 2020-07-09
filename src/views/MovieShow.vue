
<template>
  <div class="movie-show">
    <p>Title: {{ movie.title }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Director: {{ movie.director }}</p>
    <br>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get(`api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then(response => {
          console.log("Successfully destroyed", response.data);
          this.$router.push("/movies");
        });
      }
    }
  }
};
</script> 