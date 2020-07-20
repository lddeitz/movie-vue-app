<template>
  <div class="movie-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
       <div class="form-group">
          <label>Name:</label>
          <input v-model="newMovieTitle" type="text" class="form-control">
        </div>
        <div class="form-group">
          <label>Year:</label>
          <input v-model="newMovieYear" type="text" class="form-control">
        </div>
        <div class="form-group">
          <label>Plot:</label>
          <input v-model="newMoviePlot" type="text" class="form-control">
        </div>
        <div class="form-group">
          <label>Director:</label>
          <input v-model="newMovieDirector" type="text" class="form-control">
        </div>
        <input type="submit" class="btn btn-primary" value="Create">
    </form>
  </div>
</template>


<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Create a new movie:",
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    createMovie: function() {
      var params = {
        //set a variable equal to params of v-models
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector
      };
      axios.post("/api/movies", params).then(response => {
        // redirect to movies show
        this.$router.push(`/movies/${response.data.id}`).catch(error => {
          this.errors = error.response.data.errors;
        });
      });
    }
  }
};
</script>