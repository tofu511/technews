<template>
  <div class="container">
    <nav class="nav-content">
      <div class="menu">
        <ul>
          <template v-for="(site, key) in sites">
            <li :key="key">
              <nuxt-link
                :to="`${site.path}`"
                :class="{ active: isActivePath(site.path) }"
              >
                <font-awesome-icon :icon="[site.iconPrefix, site.iconName]" class="icon" />
              </nuxt-link>
            </li>
          </template>
        </ul>
      </div>
    </nav>
    <SubMenu />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import SubMenu from '@/components/SubMenu.vue'

interface Site {
  path: string
  iconPrefix: string
  iconName: string
}

@Component({
  components: {
    SubMenu
  }
})

export default class Footer extends Vue {
  sites: Array<Site> = [
    {
      path: '/',
      iconPrefix: 'fas',
      iconName: 'home'
    },
    {
      path: '/hackernews',
      iconPrefix: 'fab',
      iconName: 'hacker-news-square'
    },
    {
      path: '/dev',
      iconPrefix: 'fab',
      iconName: 'dev'
    }
  ]

  isActive: Boolean = false

  isActivePath (path: String): Boolean {
    return this.$nuxt.$route.path === path
  }
}
</script>

<style lang="scss" scoped>
.nav-content {
  background-color: #212121;
  overflow: hidden;
}

.icon {
  font-size: 24px;
  margin: 0 7px;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: hidden;
}

input {
  display: none;
}

li {
  float: left;

  a {
    color: #f5f3f2;
    text-align: center;
    padding: 14px 12px;
    text-decoration: none;
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
