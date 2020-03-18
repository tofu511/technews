<template>
  <header class="header">
    <nav class="nav-inner">
      <nuxt-link to="/">
        Home
      </nuxt-link>
      <nuxt-link v-for="(site, key) in sites" :key="key" :to="`/${site.path}`">
        {{ site.title }}
      </nuxt-link>
    </nav>
  </header>
</template>

<script lang="ts">
import Vue from 'vue'

interface Site {
  title: string
  path: string
}

export default class Footer extends Vue {
  sites: Array<Site> = [
    {
      title: 'Hacker News',
      path: 'hn'
    },
    {
      title: 'DEV',
      path: 'dev'
    }
  ]
}
</script>

<style lang="scss" scoped></style>
