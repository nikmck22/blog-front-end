<template>
  <div class="PostsShow">
    <h1>{{ message }}</h1>
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
      post: {}
    };
  },
  created: function() {
    axios.get('/api/posts' + this.$route.params.id).then(response => {
      console.log(response.data);
      this.post = response.data;
    })
  },
  methods: {}
};
</script>