<template>
  <div class="app">
    <h1>Post Page</h1>
    <my-input v-model="searchQuery" placeholder="Search..."></my-input>
    <div class="app__btns">
      <my-button @click="showDialog">create a post</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"> </my-select>
    </div>
    <!-- <my-button @click="fetchPosts"> get posts</my-button> -->

    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>

    <!-- </post-form> -->
    <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading" />
    <div v-else>Loading...</div>
    <!-- </post-list> -->
  </div>
</template>

<script>
import PostForm from "./components/PostForm.vue";
import PostList from "./components/PostList.vue";
import MyButton from "./components/UI/MyButton.vue";
import MyDialog from "./components/UI/MyDialog.vue";
import axios from "axios";
// import MySelect from './components/UI/mySelect.vue';

export default {
  components: { PostForm, PostList, MyDialog, MyButton,  },

  data() {
 
    return {
      posts: [
        // { id: 1, title: "JS", body: "description" },
        // { id: 2, title: "JS 2", body: "description 2" },
        // { id: 3, title: "JS 3", body: "description 3" },
      ],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      sortOptions: [
        {value: 'title', name: 'po nazvaniu' },
        {value: 'body', name: 'po sederzhaniu' }
      ]
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

    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },

    showDialog() {
      this.dialogVisible = true;
    },

    async fetchPosts() {
      try {
        this.isPostsLoading = true;

        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );
        console.log(response);
        this.posts = response.data;
      } catch (e) {
        alert("err");
      } finally {
        this.isPostsLoading = false;
      }
    },

    // inputTitle(event) {},
    // inputBody(event) {},
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts(){
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      })

    },
    sortedAndSearchedPosts(){
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
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

.app__btns{
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
}
</style>