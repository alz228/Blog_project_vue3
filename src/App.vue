<template>
  <div class="app">
    <h4>Create a post</h4>
    <form @submit.prevent>
      <input
        v-bind:value="title"
        @input="title = $event.target.value"
        class="input"
        type="text"
        placeholder="title"
      />
      <input
        v-bind:value="body"
        @input="body = $event.target.value"
        class="input"
        type="text"
        placeholder="description"
      />

      <button class="btn" @click="createPost">create</button>
    </form>
  

    <div class="post" v-for="post in posts">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        { id: 1, title: "JS", body: "description" },
        { id: 2, title: "JS 2", body: "description 2" },
        { id: 3, title: "JS 3", body: "description 3" },
      ],
    };
  },
  methods: {
    createPost() {
      
        const newPost = {
            id: Date.now(),
            title: this.title,
            body: this.body,
        }
        this.posts.push(newPost)
    },
    // inputTitle(event) {},
    // inputBody(event) {},
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

.input {
  width: 100%;
  border: 0.5mm solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

form {
  display: flex;
  flex-direction: column;
}

.btn {
  align-self: flex-end;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1mm solid teal;
}
</style>