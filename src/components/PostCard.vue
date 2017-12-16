<template>

  <q-card>
    <q-card-media v-if="hasFeaturedMedia">
      <img :src="getFeaturedMedia">
      <q-card-title slot="overlay">
        <span v-html="value.title.rendered"></span>
        <span slot="subtitle">{{getDate}}</span>
      </q-card-title>
    </q-card-media>
    <q-card-title v-if="!hasFeaturedMedia">
      <span v-html="value.title.rendered"></span>
      <span slot="subtitle">{{getDate}}</span>
    </q-card-title>
    <q-card-main>
      <span v-html="getFixedExcerpt"></span>
    </q-card-main>
    <q-card-separator />
    <q-card-actions>
      <q-btn color="purple" @click="readMore">Continue Reading</q-btn>
    </q-card-actions>
  </q-card>

</template>

<script>
  import {QCard, QIcon, QCardMedia, QCardTitle, QCardMain, QCardSeparator, QCardActions, QBtn} from 'quasar-framework'
  import distanceInWordsToNow from 'date-fns/distance_in_words_to_now'
  import parse from 'date-fns/parse'

  export default {
    props: ['value'],
    computed: {
      getFixedExcerpt () {
        return this.value.excerpt.rendered.replace(/<a[^>]*?>[\s\S]*?<\/a>/gi, '')
      },
      getFeaturedMedia () {
        return this.value['_embedded']['wp:featuredmedia'][0]['source_url']
      },
      hasFeaturedMedia () {
        return (this.value._embedded['wp:featuredmedia'][0] !== undefined)
      },
      getDate () {
        return distanceInWordsToNow(parse(this.value.date_gmt), {addSuffix: true})
      }
    },
    methods: {
      readMore () {
        this.$emit('more')
      }
    },
    name: 'post-card',
    components: {QCard, QIcon, QCardMedia, QCardTitle, QCardMain, QCardSeparator, QCardActions, QBtn}
  }
</script>

<style scoped>

</style>
