<template>
  <h4 :style="{'color':'#1a1a1a'}">Create a post</h4>
  <form @submit.prevent>
    <my-input :style="{'color': '#1a1a1a'}" v-focus v-model="post.title" type="text" placeholder="title" />
    <my-input :style="{'color': '#1a1a1a'}" v-model="post.body" type="text" placeholder="description" />

    <my-button
      class="btn"
      @click="createPost"

      style="align-self: flex-end; margin-top: 15px"
      >create</my-button
    >
  </form>
</template>

<script>
import toggleMixin from "@/mixins/toggleMixin";
export default {
  mixins: [toggleMixin],
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

      this.hideDialog()
    
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
