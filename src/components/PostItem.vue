<template>
  <div class="post">
    <div>
      <div class="post__title">{{ post.title }}</div>
      <div class="post__description">{{ post.body }}</div>
    </div>

    <div class="post__btns">
      <my-button @click="$router.push(`/posts/${post.id}`)">Open</my-button>
      <my-button
        @click="$emit('remove', post)"
        :style="{ 'margin-left': '15px' }"
        >Delete</my-button
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  padding: 15px;
  /* border: 2px solid teal; */
  margin-top: 15px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
  background-color: #242424;
}

.post__btns {
  display: flex;
}

@media screen and (max-width: 640px) {
  .post {
    flex-direction: column;
    align-items: start;
  }

  .post__btns {
    margin-top: 15px;
  }
}
.post__title {
  font-size: 20px;
  font-weight: bold;
  color: teal;
}

.post__description {
  margin-top: 10px;
}
</style>
