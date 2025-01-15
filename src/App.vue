<template>
  <div class="app">
    <h1>Post Page</h1>
    <my-button @click="showDialog">create a post</my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form  @create="createPost"/>
    </my-dialog>
  


  <!-- </post-form> -->
<post-list :posts="posts" @remove="removePost" />
<!-- </post-list> -->
   
  </div>
</template>

<script>
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';
import MyButton from './components/UI/MyButton.vue';
import MyDialog from './components/UI/MyDialog.vue';

export default {
    components: {PostForm, PostList, MyDialog, MyButton },

  data() {
    return {
      posts: [
        { id: 1, title: "JS", body: "description" },
        { id: 2, title: "JS 2", body: "description 2" },
        { id: 3, title: "JS 3", body: "description 3" },
      ],
      dialogVisible: false,
    };
  },
  methods: {
    createPost(post) {
      
        this.posts.push(post);

        // const newPost = {
        //     id: Date.now(),
        //     title: this.title,
        //     body: this.body,
        // }
        // this.posts.push(newPost)
        // this.title = ''
        // this.body = ''
    },

    removePost(post){
      this.posts = this.posts.filter(p => p.id !== post.id)
    },

    showDialog(){
      this.dialogVisible = true
    }
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


</style>