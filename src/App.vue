<template>
  <!-- Don't drop "q-app" class -->
  <div id="q-app">
    <router-view />
  </div>
</template>

<script>
/*
 * Root component
 */
import {Loading, QSpinnerAudio} from 'quasar-framework'
export default {
  methods: {
    showLoading () {
      Loading.show({
        spinner: QSpinnerAudio,
        message: 'Preparing',
        messageColor: 'white',
        spinnerSize: 100, // in pixels
        spinnerColor: 'white'
      })
    },
    hideLoading () {
      Loading.hide()
    }
  },
  created () {
    this.$q.events.$on('loading:start', this.showLoading)
    this.$q.events.$on('loading:end', this.hideLoading)
  }
}
</script>

<style></style>
