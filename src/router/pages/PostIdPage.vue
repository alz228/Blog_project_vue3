<template>
  <div>
    <h2>Post Details:</h2>
    <p v-if="postId" style="margin-top: 30px">
      Post id: <strong>{{ postId }}</strong>
    </p>

    <div v-if="isPostsLoading">
      <p>Loading post details...</p>
    </div>

    <div v-else-if="post">
      <p class="postpage__title">
        Title:<strong>{{ post.title }}</strong>
      </p>
      <p class="postpage__description">
        Description: <strong>{{ post.body }}</strong>
      </p>
    </div>

    <div v-else>
      <p>Post not found</p>
    </div>

    <my-button @click="$router.push('/blog')" style="margin-top: 15px"
      >Back to blog</my-button
    >
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  computed: {
    postId() {
      return Number(this.$route.params.id);
    },
    ...mapState("post", ["posts", "isPostsLoading"]),
    post() {
      if (!this.posts || !Array.isArray(this.posts)) {
        return null;
      }
      return this.posts.find((post) => post.id === this.postId) || null;
    },
  },
  created() {
    console.log("PostId from route:", this.postId);
    console.log("Posts from Vuex:", this.posts);
    if (!this.posts || !Array.isArray(this.posts) || this.posts.length === 0) {
      this.fetchPosts();
    }
  },
  methods: {
    ...mapActions("post", ["fetchPosts"]),
  },
};
</script>

<style scoped></style>

<style scoped>
.postpage__title {
  font-weight: bold;
  font-size: 28px;
  margin-top: 15px;
}

.postpage__description {
  margin-top: 15px;
}
</style>
