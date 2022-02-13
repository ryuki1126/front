<template>
  <div>
    <v-card
      class="my-3 px-10"
      min-height=150vh
    >
      <div class="pt-10 pl-10">
        <v-card-title class="text-h3">
          {{ posts.article_title }}
        </v-card-title>
        <v-card-subtitle class="pt-5">
          作成日 : {{ posts.created_at }} , 更新日 : {{ posts.updated_at }}
        </v-card-subtitle>
      </div>
      <div class="pl-10 mt-10" v-html="$md.render(content)"></div>
    </v-card>
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
        const created_at = res.data.created_at.substr(0, 10)
        const updated_at = res.data.updated_at.substr(0, 10)
        res.data.created_at = created_at
        res.data.updated_at = updated_at
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