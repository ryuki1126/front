<template>
  <div>
    <div>
        <p v-for="post in posts" :key=post.id>
            {{ post.article_title }}
        </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      posts: '',
    }
  },
  mounted() {
    axios.get('http://localhost:8000/api/articles')
      .then((res) => {
        this.posts = res.data
      })
      .catch((error) => {
        console.log(error)
        this.posts = 'error'
      })
  }
}
</script>
