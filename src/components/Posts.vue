<template>
  <div id="posts" class="row">
    <div class="col-12">
      <div></div>
      <h1>Posts:</h1>

      <div v-if="posts.length === 0" class="col-12 text-center">
        <b-spinner label="Spinning"></b-spinner>&nbsp;loading...
      </div>

      <div v-else v-for="p in posts" :key="p.id" class="post col-lg-12">
        <div class="post__bg p-3">
          <h2>
            <small class="small text-muted"># {{ p.id }} </small> {{ p.title }}
          </h2>

          <p>{{ p.body }}</p>

          <PostUser :id="p.userId" />

          <PostsComments :postId="p.id" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
import PostsComments from "./PostsComments.vue";
import PostUser from "./PostUser.vue";
// import UserAvatar from "./UserAvatar.vue";

export default {
  components: { PostsComments, PostUser },

  props: {
    posts: Array,
    userId: Number,
    postId: Number,
  },

  data() {
    return {
      comments: [],
      users: [],
    };
  },

  // methods: {
  // getPostComments() {
  //   return this.comments.filter((comment) => comment.postId === this.postId);
  // },
  // async loadComments() {
  //   await axios
  //     .get("https://jsonplaceholder.typicode.com/comments")
  //     .then((response) => {
  //       this.comments = response.data;
  //     });
  // },
  // async loadUsers() {
  //   await axios
  //     .get("https://jsonplaceholder.typicode.com/users", {
  //       params: {
  //         userId: this.userId,
  //         postId: this.postId,
  //       },
  //     })
  //     .then((response) => {
  //       this.users = response.data;
  //     });
  // },
  // },
};
</script>
 
