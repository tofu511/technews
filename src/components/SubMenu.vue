<template>
  <div class="container">
    <ul>
      <template v-for="(path, key) in getLinksFromPath(currentPath)">
        <li :key="key">
          <nuxt-link :to="`/${currentPath}/${path}`">
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
      ['hackernews', ['news', 'newest', 'ask', 'show', 'jobs']],
      ['dev', ['rising', 'week', 'month', 'year', 'podcast']]
    ])

    get currentPath (): String {
      return this.$nuxt.$route.path.substr(1)
    }

    getLinksFromPath (path: String): Array<String> {
      let key
      if (path.includes('/')) {
        key = path.slice(0, path.indexOf('/'))
      } else {
        key = path
      }
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
</style>
