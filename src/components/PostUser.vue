<template>
  <div id="users" class="row">
    <div class="col-12">
      <h1 class="col-12">Author:</h1>
      <b-button @click="toogleUsersOpen()" variant="primary"
        >{{ isUserOpen ? "Hide" : "Show" }}
      </b-button>
      <b-collapse v-model="isUserOpen">
        <div v-for="user in users" :key="user.id" class="col-12">
          <b-avatar variant="warning" class="icon">{{ user.id }}</b-avatar>
          <p class="user">Name - {{ user.name }}</p>
          <p class="user">lastName - {{ user.username }}</p>
          <p class="user">Email - {{ user.email }}</p>
        </div>
      </b-collapse>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    id: Number,
  },

  data() {
    return {
      isUserOpen: false,
      users: [],
    };
  },

  async mounted() {
    await this.loadUsers();
  },

  methods: {
    async loadUsers() {
      await axios
        .get("https://jsonplaceholder.typicode.com/users", {
          params: {
            id: this.id,
          },
        })
        .then((response) => {
          this.users = response.data;
        });
    },

    toogleUsersOpen() {
      this.isUserOpen = !this.isUserOpen;
    },
  },
};
</script>
<style>
.user {
  text-decoration-line: overline;
}
</style>