<template>
  <div class="h-full">
    <div>
      <v-card
        class="my-3"
        v-for="post in posts" :key=post.id
        outlined
        hover
      >
        <v-card-title class="text-h5">
          {{ post.article_title }}
        </v-card-title>
        <v-card-subtitle>
          作成日 : {{ post.created_at }} , 更新日 : {{ post.updated_at }}
        </v-card-subtitle>
        <v-card-subtitle>記事内容の説明文をここに記載</v-card-subtitle>
        <v-card-actions>
          <nuxt-link class="pointer" tag="div" :to="`article/${post.id}`">
            <v-btn
            text
            color="main"
            >
              記事を読む
            </v-btn>
          </nuxt-link>
        </v-card-actions>
      </v-card>
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
  async fetch() {
    const res = await axios.get('http://localhost:8000/api/articles')
    for(let i = 0; i < res.data.length; i++) {
      const created_at = res.data[i].created_at.substr(0, 10)
      const updated_at = res.data[i].updated_at.substr(0, 10)
      res.data[i].created_at = created_at
      res.data[i].updated_at = updated_at
    }
    this.posts = res.data
  },
}
</script>

<style scoped>
  .pointer {
    cursor: pointer;
  }
  .h-full {
    min-height: 100vh;
  }
</style>