<template>

  <div class="layout-padding">

      <q-infinite-scroll :handler="loadMore">

        <post-card v-for="(post, index) in posts" :key="index" v-model="posts[index]" @more="readMore(index)"></post-card>
        <div slot="message" class="row justify-center" style="margin-bottom: 50px;">
          <q-spinner-dots :size="40" />
        </div>
      </q-infinite-scroll>

    <post v-model="getSelectedPost"></post>

  </div>

</template>

<script>
  import axios from 'axios'
  import PostCard from './PostCard'
  import Post from './Post'
  import {QPullToRefresh, QSpinnerDots, QInfiniteScroll, Events} from 'quasar-framework'

  export default {
    computed: {
      getSelectedPost () {
        return this.posts[this.selectedPost]
      }
    },
    methods: {
      readMore (index) {
        this.selectedPost = index
        Events.$emit('post:read')
      },
      loadMore (index, done) {
        this.updatePosts(index + 1)
          .then(() => { done() })
      },
      updatePosts (index) {
        const url = `${process.env.WP_BASE}/wp-json/wp/v2/posts?_embed&page=${index}` // + (!category) ? '' : '?category=' + category
        console.log('url', url)
        return axios.get(url)
          .then(res => {
            console.log(res)
            this.posts = this.posts.concat(res.data)
          })
      }
    },
    created () {
    },
    data () {
      return {
        posts: [],
        selectedPost: null
      }
    },
    components: {Post, PostCard, QPullToRefresh, QSpinnerDots, QInfiniteScroll},
    name: 'list'
  }
</script>

<style scoped>

</style>
