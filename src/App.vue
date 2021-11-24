<template>
  <div id="app" class="container">
    <HeaderBlock title="Lesson 7" text="Automation" />
    <div id="posts">
      <b-pagination
        v-model="currentPage"
        :total-rows="posts.length"
        :per-page="perPage"
        aria-controls="my-table"
      ></b-pagination>

      <Posts :posts="paginatedPosts" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import HeaderBlock from "./components/HeaderBlock.vue";
import Posts from "./components/Posts.vue";

export default {
  name: "App",
  components: {
    HeaderBlock,
    Posts,
  },
  data() {
    return {
      email: "",
      posts: [],
      currentPage: 1,
      perPage: 5,
    };
  },
  async mounted() {
    await this.loadPosts();
  },

  computed: {
    paginatedPosts() {
      const start = this.currentPage > 1 ? this.currentPage * this.perPage : 0; // 0 - начало массива
      return this.posts.slice(start, start + this.perPage);
    },
  },

  methods: {
    async loadPosts() {
      this.posts = [];
      await axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then((response) => {
          this.posts = response.data;
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

