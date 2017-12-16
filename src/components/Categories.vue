<template>
  <q-list highlight no-border>
    <q-list-header>
      Quick Links
    </q-list-header>
    <q-item @click="go('/about')">
      About Us
    </q-item>
    <q-item @click="go('/')">
      Latest Posts
    </q-item>

    <q-item-separator />

    <q-list-header>Categories</q-list-header>
    <q-item v-for="(category, index) in categories" :key="index" @click="go('/category/' + category.id)" >
      {{category.name}} ({{category.count}} posts)
    </q-item>
  </q-list>
</template>

<script>
  import {QList, QItem, QListHeader, QItemSeparator, Events, Toast} from 'quasar-framework'
  import axios from 'axios'
  export default {
    computed: {
    },
    methods: {
      go (url) {
        console.log('goto', url)
        this.$router.push(url)
        Events.$emit('side:toggle')
      }
    },
    data () {
      return {
        categories: []
      }
    },
    mounted () {
      axios.get(process.env.WP_BASE + '/wp-json/wp/v2/categories?parent=0')
        .then(res => {
          this.categories = res.data
        })
        .catch(() => {
          Toast.create.negative('Whoops! Something went wrong updating the categories.')
        })
    },
    name: 'categories',
    components: {QList, QItem, QListHeader, QItemSeparator}
  }
</script>

<style scoped>

</style>
