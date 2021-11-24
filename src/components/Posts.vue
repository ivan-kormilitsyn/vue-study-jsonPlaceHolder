<template>
  <div id="posts" class="row">
    <div class="col-12">
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
          <UserToDo :userId="p.userId" />
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
import UserToDo from "./UserToDo.vue";

export default {
  components: { PostsComments, PostUser, UserToDo },

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
};
</script>
 
