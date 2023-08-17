<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<template>
  <div class="post">
    <div>
    <div><strong>Название: </strong>{{ post.title }}</div>
    <div><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <div class="post_btns">
      <MyButton @click="$emit('remove', post)">Delete</MyButton>
    </div>
  </div>
</template>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid green;
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.post_btns {
  background: none;
  border-radius: 0;
  align-self: flex-end;
}
</style>