<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h4>This is the Posts Index page</h4>
        <!-- Find your post here: <input type="text" v-model="titleFilter"> -->

      <div v-for="post in filterBy(posts, $parent.titleFilter, 'title')" v-on:click="currentPost = post" v-bind:class="{selected: currentPost === post}">   
        <p>{{ post.id }} - Title: {{ post.title }}</p>
        <p>{{ post.body }}</p>
        <p>{{ post.image }}</p>
      </div>
  </div>
</template>

<style>
.selected {
  color: white;
  background-color: blueviolet;
}

</style>
<script>
import Vue2Filters from "vue2-filters";
import axios from "axios";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
      currentPost: {},
      titleFilter: ''
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