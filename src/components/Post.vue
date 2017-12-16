<template>

  <q-modal ref="layoutModal" maximized>
    <q-modal-layout >
      <q-toolbar slot="header" color="purple">
        <q-btn flat @click="$refs.layoutModal.close()">
          <q-icon name="keyboard_arrow_left" />
          Back
        </q-btn>
        <div class="q-toolbar-title">
        </div>
      </q-toolbar>
      <div class="layout-padding">
        <h5><span v-html="value.title.rendered"></span></h5>
        <!--<img :src="getFeaturedMedia" v-if="hasFeaturedMedia" width="100%" />-->
        <span v-html="value.content.rendered"></span>
      </div>
    </q-modal-layout>
  </q-modal>

</template>

<script>
  import {Events, QModalLayout, QModal, QToolbar, QBtn, QIcon} from 'quasar-framework'
  export default {
    computed: {
      getFeaturedMedia () {
        return this.value['_embedded']['wp:featuredmedia'][0]['source_url']
      },
      hasFeaturedMedia () {
        return (this.value._embedded['wp:featuredmedia'][0] !== undefined)
      }
    },
    props: ['value'],
    name: 'post',
    components: {QModalLayout, QModal, QToolbar, QBtn, QIcon},
    mounted () {
      Events.$on('post:read', () => { this.$refs.layoutModal.open() })
    },
    destroyed () {
      Events.$off('post:read')
    }
  }
</script>

<style scoped>

</style>
