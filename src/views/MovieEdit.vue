<template>
  <div class="movie-edit">
    
    <form v-on:submit.prevent="editMovie()">
      <h1>Edit Movie</h1>

      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="movie.title">
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="movie.year">
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="movie.plot">
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="movie.director">
      </div>
      <input type="submit" class="btn btn-primary" value="Update">
    </form>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      errors: [],
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    editMovie: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director
      };
      axios.patch(`/api/movies/${this.movie.id}`, params).then(response => {
        // redirect to movies show
        this.$router.push(`/movies/${response.data.id}`);
      });
    }
  }
};
</script>