<template>
  <div>
    <div>
        <h1>
          {{id}}
        </h1>
        <div class="mt-4" v-html="$md.render(content)"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      id: '',
      posts: '',
      content: '',
    }
  },
  created() {
    this.id = this.$route.params.id
  },
  mounted() {
    const url = 'http://localhost:8000/api/article/' + this.id
    console.log(url)
    axios.get(url)
      .then((res) => {
        console.log(res.data)
        this.content = res.data.article_content
        this.posts = res.data
      })
      .catch((error) => {
        console.log(error)
        this.posts = 'error'
      })
  }
}
</script>