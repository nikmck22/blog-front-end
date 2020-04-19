<template>
  <div class="PostsEdit">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Edit this post</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Title:</label> 
          <input type="text" class="form-control" v-model="post.title">
        </div>
        <div class="form-group">
          <label>Body:</label>
          <input type="text" class="form-control" v-model="post.body">
        </div>
        <div class="form-group">
          <label>Image:</label>
          <input type="text" class="form-control" v-model="post.image">
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

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {
        title: "",
        body: "",
        image: "",
      },
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.post.title,
        body: this.post.body,
        image: this.post.image
      };
      axios
        .patch(`/api/posts/${this.post.id}/edit`, params)
        .then(response => {
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>