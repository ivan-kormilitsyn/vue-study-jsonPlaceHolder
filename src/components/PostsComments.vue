<template>
  <div id="comments" class="row">
    <div class="col-12">
      <h1>Comments:</h1>

      <b-button @click="toogleCommentsOpen()" variant="primary">{{
        isCommentsOpen ? "Hide" : "Show"
      }}</b-button>
      <b-collapse v-model="isCommentsOpen" class="mt-2">
        <div v-for="comment in comments" :key="comment.id" class="comment">
          <p>ID - {{ comment.id }}</p>
          <p>Author - {{ comment.name }}</p>
          <p>Email - {{ comment.email }}</p>
          <p>Text - {{ comment.body }}</p>
        </div>
      </b-collapse>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    postId: Number,
  },

  data() {
    return {
      isCommentsOpen: false,
      comments: [],
    };
  },

  async mounted() {
    await this.loadComments();
  },

  methods: {
    async loadComments() {
      await axios
        .get("https://jsonplaceholder.typicode.com/comments", {
          params: {
            postId: this.postId,
          },
        })
        .then((response) => {
          this.comments = response.data;
        });
    },
    toogleCommentsOpen() {
      this.isCommentsOpen = !this.isCommentsOpen;
    },
  },
};
</script>

<style>
.comment {
  text-decoration-line: underline;
  box-shadow: 0px 0px 8px 4px #ff3c2229;
}
</style>