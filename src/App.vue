<template>
  <div class="app">
    <h1>Posts page</h1>

    <div class="app_btns">
      <MyButton @click="showDialog">Create post</MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions"/>
    </div>

    <PostList :posts="posts" v-if="!isPostLoading" @remove="removePost"/>
    <div v-else>Loading ...</div>

    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost" />
    </MyDialog>

  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyDialog from "@/components/UI/MyDialog.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: {
    MySelect,
    MyButton,
    MyDialog,
    PostForm,
    PostList,
    axios
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'by name'},
        {value: 'body', name: 'by value'}
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = response.data;
      } catch (e) {
        alert('Error')
      } finally {
        this.isPostLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  margin: 15px;
}
.app_btns {
  display: flex;
  justify-content: space-between;
  margin: 10px 0;
}
</style>
