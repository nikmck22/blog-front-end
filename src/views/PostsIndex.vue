<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h4>This is the Posts Index page</h4>
        Find your post here: <input type="text" v-model="titleFilter" list="titles">
        <datalist id="titles">
          <option v-for="post in posts">{{post.title}}</option>
        </datalist>

        <button v-on:click="setSortAttribute('title')"> Sort by title</button>
        <button v-on:click="setSortAttribute('body')"> Sort by body</button>
        <button v-on:click="setSortAttribute('image')"> Sort by image</button>

       <transition-group appear enter-active-class="animated pulse" leave-active-class="bounceOut">
          <div v-for="post in orderBy(filterBy(posts, titleFilter, 'title'), sortAttribute, 'title', 1)" v-on:click="currentPost = post" 
          v-bind:class="{selected: currentPost === post}"
          v-bind:key="post.id"
          >   
            <p>{{ post.id }} - {{ post.title }}</p>
            <p>{{ post.body }}</p>
            <p>{{ post.image }}</p>
          
        </div>
      </transition-group>
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
      titleFilter: '',
      sortAttribute: "title"
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      console.log(response.data);
      this.posts = response.data;
    }
    );
  },
  methods: {
    setSortAttribute: function(attribute) {
      console.log(attribute);
      console.log('setting sort attribute');
      this.sortAttribute = attribute;
    }
  }
};
</script>