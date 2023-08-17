
<template>
  <div v-if="posts.length > 0">
    <h3>Posts</h3>
    <PostItem v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)"/>
  </div>
  <div v-else style="color: red"><h3>Empty posts</h3></div>
</template>

<script>
import PostItem from "@/components/PostItem.vue";
export default {
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>

</style>