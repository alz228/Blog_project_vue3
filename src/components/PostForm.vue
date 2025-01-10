<template>
  <h4>Create a post</h4>
  <form @submit.prevent>
    <my-input v-model="post.title" type="text" placeholder="title" />
    <my-input v-model="post.body" type="text" placeholder="description" />

    <my-button
      class="btn"
      @click="createPost"
      style="align-self: flex-end; margin-top: 15px"
      >create</my-button
    >
  </form>
</template>

<script>
// import MyButton from './UI/MyButton.vue'

export default {
  // components: {
  //     MyButton
  // },
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);

      this.post = {
        title: "",
        body: "",
      };

      // this.posts.push(newPost)
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>