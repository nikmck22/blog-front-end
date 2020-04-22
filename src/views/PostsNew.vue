<template>
  <div class="PostsNew">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Add a New Post</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <img v-if="status" v-bind:src="`https://http.cat/${status}`">
        <div class="form-group">
          <label>Title:</label> 
          <input type="text" class="form-control" v-model="title">

          <small v-if="title.length <= 20">{{ 20 - title.length }} characters remaining</small>
          <small v-if="title.length > 20" class="alert alert-danger">Title must be less than 20 characters</small>
        </div>
        <div class="form-group">
          <label>Body:</label>
          <input type="text" class="form-control" v-model="body">
        </div>
        <div class="form-group">
          <label>Image:</label>
          <input type="text" class="form-control" v-model="image">
        </div>
        <!-- <div class="form-group">
          <label>Password confirmation:</label>
          <input type="text" class="form-control" v-model="passwordConfirmation">
        </div> -->
        <input type="submit" class="btn btn-primary" value="Submit">
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
      title: "",
      body: "",
      image: "",
      errors: [],
      status: ""
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image
      };
      axios
        .post("/api/posts", params)
        .then(response => {
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    }
  }
};
</script>