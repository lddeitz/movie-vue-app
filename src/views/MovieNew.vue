
<template>
  <div class="movie-new">
    <h1>{{ message }}</h1>
    <div>
      <form v-on:submit.prevent="createMovie()">
        <h1>New Movie</h1>
        <!-- <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul> -->
        <div class="form-group">
          <label>Title:</label>
          <input type="text" class="form-control" v-model="newMovieTitle">
        </div>
        <div class="form-group">
          <label>Year:</label>
          <input type="text" class="form-control" v-model="newMovieYear">
        </div>
        <div class="form-group">
          <label>Plot:</label>
          <input type="text" class="form-control" v-model="newMoviePlot">
        </div>
        <div class="form-group">
          <label>Director:</label>
          <input type="text" class="form-control" v-model="newMovieDirector">
        </div>
        <input type="submit" class="btn btn-primary" value="Create">
    </form>
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
      message: "Create a new movie:",
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: ""
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
        this.$router.push(`/recipes/${response.data.id}`);
      });
    }
  }
};
</script>