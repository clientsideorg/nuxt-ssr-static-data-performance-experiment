<template>
  <div class="posts-wrapper">
    <div class="post" :style="`border: 1px solid ${color}`" v-for="post of posts" :key="post.id">
      {{post.title}}
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      color: {
        type: String,
        default: 'green'
      },
      posts: {
        type: Array,
        required: true
      }
    }
  }
</script>
<style scoped>

</style>
