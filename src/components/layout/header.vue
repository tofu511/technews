<template>
  <header class="header">
    <nav class="nav-inner">
      <ul>
        <template v-for="(site, key) in sites">
          <li :key="key">
            <nuxt-link
              :to="`${site.path}`"
              :class="{ active: isActivePath(site.path) }"
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
      path: '/'
    },
    {
      title: 'Hacker News',
      path: '/hn'
    },
    {
      title: 'DEV',
      path: '/dev'
    }
  ]

  isActive: Boolean = true

  isActivePath (path: String): Boolean {
    return this.$nuxt.$route.path === path
  }
}
</script>

<style lang="scss" scoped>
.nav-inner {
  background-color: #212121;

  ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

li {
  float: left;

  a {
    color: #f5f3f2;
    text-align: center;
    padding: 14px 12px;
    text-decoration: none;
    &:hover {
      opacity: 0.5;
    }
    &.active {
      color: #00bfa5;
    }
  }
}
}

</style>
