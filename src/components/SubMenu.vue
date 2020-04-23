<template>
  <div class="container">
    <ul>
      <template v-for="(path, key) in siteLinks">
        <li :key="key">
          <nuxt-link
            :to="`/${siteName}/${path}`"
            :class="{ active: isActivePath(path) }"
          >
            {{ path }}
          </nuxt-link>
        </li>
      </template>
    </ul>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-property-decorator'

export default class SubMenu extends Vue {
    links: Map<String, Array<String>> = new Map([
      ['hackernews', ['news', 'newest', 'show', 'jobs']],
      ['dev', ['rising', 'week', 'month', 'year']]
    ])

    isActive: Boolean = false

    isActivePath (path: String): Boolean {
      const current = this.currentPath
      return current.slice(current.indexOf('/') + 1, current.length) === path
    }

    get currentPath (): String {
      return this.$nuxt.$route.path.substr(1)
    }

    get siteName (): String {
      const path = this.$nuxt.$route.path.substr(1)
      let site
      if (path.includes('/')) {
        site = path.slice(0, path.indexOf('/'))
      } else {
        site = path
      }
      return site
    }

    get siteLinks (): Array<String> {
      const key = this.siteName
      const links = this.links.get(key)
      if (links) {
        return links
      } else {
        return []
      }
    }
}

</script>

<style lang="scss" scoped>
.container {
  background-color: #212121;
}

ul {
  list-style-type: none;
  overflow: hidden;
  margin: -10px 0 0 0;
  padding: 0;
}

li {
  float: left;
  a {
    display: block;
    text-align: center;
    text-decoration: none;
    color: white;
    font-size: 18px;
    padding: 0 10px;
    transition: 100ms;
    &:hover {
      opacity: 0.5;
    }
    &.active {
      color: #00bfa5;
    }
  }
}

</style>
