<template>
  <header class="header">
    <nav class="nav-inner">
      <ul>
        <template v-for="(site, key) in sites">
          <li :key="key">
            <nuxt-link
              :to="`/${site.path}`"
              :class="{ active: activeSite(site.title, key) }"
            >
              {{ site.title }}
            </nuxt-link>
          </li>
        </template>
      </ul>
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
      title: 'Home',
      path: ''
    },
    {
      title: 'Hacker News',
      path: 'hn'
    },
    {
      title: 'DEV',
      path: 'dev'
    }
  ]

  isActive: Boolean = true

  activeSite (siteTitle: String, index: number): Boolean {
    const hoge = this.sites[index].title
    const fuga = siteTitle
    return hoge === fuga
  }
}
</script>

<style lang="scss" scoped>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #212121;
}

li {
  float: left;

  a {
    color: #f5f3f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    &:hover {
      opacity: 0.5;
    }
    &.active {
      color: #00bfa5;
    }
  }
}
</style>
