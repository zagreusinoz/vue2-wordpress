<template>
  <q-layout ref="layout" view="hHh LpR lFf" :right-breakpoint="1100">
    <!-- Header -->
    <q-toolbar slot="header" color="purple">
      <q-toolbar-title>
        {{ getName }}
      </q-toolbar-title>
      <q-btn flat @click="$refs.layout.toggleRight()">
        <q-icon name="menu" />
      </q-btn>
    </q-toolbar>
    <!-- Navigation -->
    <!--<q-tabs slot="navigation">-->
      <!--<q-route-tab slot="title" icon="view_quilt" to="/test-layout/about" replace hide="icon" label="About" />-->
      <!--<q-route-tab slot="title" icon="view_day" to="/test-layout/toolbar" replace hide="icon" label="Toolbar" />-->
      <!--<q-route-tab slot="title" icon="view_day" to="/test-layout/tabs" replace label="Tabs" />-->
      <!--<q-route-tab slot="title" icon="input" to="/test-layout/drawer" replace label="Drawer" />-->
    <!--</q-tabs>-->

    <!-- Right Side Panel -->
    <div slot="right">
      <categories></categories>
    </div>
    <!-- sub-routes get injected here: -->
    <router-view />

  </q-layout>
</template>

<script>
  import {QLayout, QToolbar, QToolbarTitle, QSideLink, QItemSide, QItemMain, QTabs, QRouteTab, QBtn, QIcon} from 'quasar-framework'
  import Categories from './Categories'

  export default {
    computed: {
      getName () {
        return process.env.BLOG_NAME
      }
    },
    mounted () {
      this.$q.events.$on('side:toggle', () => { this.$refs.layout.toggleRight() })
    },
    destroyed () {
      this.$q.events.$off('side:toggle')
    },
    name: 'layout',
    components: {
      Categories, QLayout, QToolbar, QToolbarTitle, QSideLink, QItemSide, QItemMain, QTabs, QRouteTab, QBtn, QIcon}
  }
</script>

<style scoped>

</style>
