<template>
  <div class="PostsShow">
    <h3>Title: {{ post.title }}</h3>
    <h3>Body: {{ post.body }}</h3>
    <h3>Image: {{ post.image }}</h3>

    <button v-on:click="deletePost()">Delete this post</button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {}
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.post.id}`).then(response => {
      console.log(response.data);
      this.post = response.data;
    })
  },
  methods: {}
};
</script>