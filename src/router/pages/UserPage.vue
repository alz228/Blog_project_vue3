<!-- old page, before decomposition -->
<template>
  <div>
    <h1>Post Page</h1>
    <my-input v-focus v-model="searchQuery" placeholder="Search..."></my-input>
    <div class="app__btns">
      <my-button @click="showDialog">create a post</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"> </my-select>
    </div>

    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>

    <post-list
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else>Loading...</div>

    <div v-intersection="loadMorePosts" class="observer"></div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyButton from "@/components/UI/MyButton.vue";
import MyDialog from "@/components/UI/MyDialog.vue";
import axios from "axios";

export default {
  components: { PostForm, PostList, MyDialog, MyButton },

  data() {
    return {
      posts: [],
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
      }
    },
  },
  mounted() {
    this.fetchPosts();
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
  watch: {},
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
