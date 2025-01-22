<template>
  <div>
    <p>Post № {{ postId }}</p>
    <h2>Post Details:</h2>
    <div v-if="post">
      <p><strong>Title:</strong> {{ post.title }}</p>
      <p><strong>Description:</strong> {{ post.body }}</p>
    </div>
    <div v-else-if="posts.length === 0">
      <p>Loading post details...</p>
    </div>
    <div v-else>
      <p>Post not found</p>
    </div>
    <my-button @click="$router.push('/blog')" style="margin-left: 15px">Blog</my-button>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  computed: {
    postId() {
      return Number(this.$route.params.id);
    },
    ...mapState('postModule', ['posts']),
    post() {
      return this.posts && this.posts.length
        ? this.posts.find((post) => post.id === this.postId)
        : null;
    },
  },
  created() {
    if (this.posts.length === 0) {
      this.fetchPosts();
    }
  },
  methods: {
    ...mapActions('postModule', ['fetchPosts']),
  },
};
</script>

<style scoped>
/* h1 {
  color: #333;
}

p {
  font-size: 18px;
}

a {
  display: inline-block;
  margin-top: 20px;
  color: #007bff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
} */
</style>