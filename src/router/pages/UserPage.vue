<template>
    <div >
      <h1>Post Page</h1>
      <my-input v-focus v-model="searchQuery" placeholder="Search..."></my-input>
      <div class="app__btns">
        <my-button @click="showDialog">create a post</my-button>
        <my-select v-model="selectedSort" :options="sortOptions"> </my-select>
      </div>
      <!-- <my-button @click="fetchPosts"> get posts</my-button> -->
  
      <my-dialog v-model:show="dialogVisible">
        <post-form @create="createPost" />
      </my-dialog>
  
      <!-- </post-form> -->
      <post-list
        :posts="sortedAndSearchedPosts"
        @remove="removePost"
        v-if="!isPostsLoading"
      />
      <div v-else>Loading...</div>
  
      <div v-intersection="loadMorePosts" class="observer"></div>
  
      <!-- zdes dekompoziciu sdelat -->
      <!-- <div class="page__wrapper">
        <div
          v-for="pageNumber in totalPages"
          :key="pageNumber"
          class="page"
          :class="{ 'current-page': page === pageNumber }"
          @click="changePage(pageNumber)"
        >
          {{ pageNumber }}
        </div>
      </div> -->
      <!-- </post-list> -->
    </div>
  </template>
  
  <script>
  import PostForm from "@/components/PostForm.vue";
  import PostList from "@/components/PostList.vue";
  import MyButton from "@/components/UI/MyButton.vue";
  import MyDialog from "@/components/UI/MyDialog.vue";
  import axios from "axios";
  // import MySelect from './components/UI/mySelect.vue';
  
  export default {
    components: { PostForm, PostList, MyDialog, MyButton },
  
    data() {
      return {
        posts: [
          // { id: 1, title: "JS", body: "description" },
          // { id: 2, title: "JS 2", body: "description 2" },
          // { id: 3, title: "JS 3", body: "description 3" },
        ],
        dialogVisible: false,
        isPostsLoading: false,
        selectedSort: "",
        searchQuery: "",
        page: 1,
        limit: 10,
        totalPages: 0,
        sortOptions: [
          { value: "title", name: "po nazvaniu" },
          { value: "body", name: "po sederzhaniu" },
        ],
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
  
      // changePage(pageNumber){
      //   this.page = pageNumber
  
      // },
      async fetchPosts() {
        try {
          this.isPostsLoading = true;
  
          const response = await axios.get(
            "https://jsonplaceholder.typicode.com/posts",
            {
              params: {
                _page: this.page,
                _limit: this.limit,
              },
            }
          );
          console.log(response);
  
          this.totalPages = Math.ceil(
            response.headers["x-total-count"] / this.limit
          );
  
          this.posts = response.data;
        } catch (e) {
          alert("err");
        } finally {
          this.isPostsLoading = false;
        }
      },
  
      async loadMorePosts() {
        try {
          this.page += 1;
          // this.isPostsLoading = true;
  
          const response = await axios.get(
            "https://jsonplaceholder.typicode.com/posts",
            {
              params: {
                _page: this.page,
                _limit: this.limit,
              },
            }
          );
          console.log(response);
  
          this.totalPages = Math.ceil(
            response.headers["x-total-count"] / this.limit
          );
  
          this.posts = [...this.posts, ...response.data];
        } catch (e) {
          alert("err");
        } finally {
          // this.isPostsLoading = false;
        }
      },
  
      // inputTitle(event) {},
      // inputBody(event) {},
    },
    mounted() {
      this.fetchPosts();
  
      // const options = {
      //   rootMargin: "0px",
      //   threshold: 1.0,
      // };
  
      // const callback = (entries, observer) => {
      //   if (entries[0].isIntersecting && this.page < this.totalPages) {
      //     this.loadMorePosts();
      //   }
      // };
      // const observer = new IntersectionObserver(callback, options);
      // observer.observe(this.$refs.observer);
    },
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => {
          return post1[this.selectedSort]?.localeCompare(
            post2[this.selectedSort]
          );
        });
      },
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter((post) =>
          post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      },
    },
    watch: {
      // page(){
      //   this.fetchPosts()
      // }
    },
  };
  </script>
  
  <style>

  
  .app__btns {
    display: flex;
    justify-content: space-between;
    margin-top: 15px;
  }
  
  .page__wrapper {
    display: flex;
    margin-top: 15px;
  }
  
  .page {
    border: 1px solid black;
    padding: 10px;
  }
  
  .current-page {
    border: 2px solid teal;
  }
  
  .observer {
    height: 30px;
    background-color: red;
  }
  </style>
  