<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h4>This is the Posts Index page</h4>
      <div v-for="post in posts">   
        <p>{{ post.id }} - Title: {{ post.title }}</p>
        <p>{{ post.body }}</p>
        <p>{{ post.image }}</p>
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
      message: "Welcome to Vue.js!",
      posts: []
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      console.log(response.data);
      this.posts = response.data;
    }
    );
  },
  methods: {}
};
</script>