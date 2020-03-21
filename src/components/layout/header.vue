<template>
  <header class="header">
    <div class="nav-wrapper">
      <nav class="nav-inner">
        <div class="menu-toggle">
          <input type="checkbox">
          <span />
          <span />
          <span />
        </div>
        <ul class="menu">
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
    </div>
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
.header {
  background-color: #212121;
  overflow: hidden;
}

@include laptop {
    ul {
      margin: 0;
      padding: 10px 0 10px 0;
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
  }

@include mobile {
  .nav-wrapper {
    display: flex;
    align-items: center;
    margin: 0;
    padding: 0;
    height: 65px;
  }

  .menu-toggle {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 25px;
    left: 25px;
    z-index: 1;
    -webkit-user-select: none;
    user-select: none;

    input {
      display: flex;
      position: absolute;
      width: 30px;
      height: 20px;
      cursor: pointer;
      opacity: 0;
      z-index: 2;

      &:checked ~ span {
        opacity: 1;
        transform: rotate(45deg) translate(-3px, -1px);
        background: #36383F;
      }
    }

    span {
      display: flex;
      width: 29px;
      height: 2px;
      margin-bottom: 5px;
      position: relative;
      background: #f5f3f2;
      border-radius: 3px;
      z-index: 1;
      transform-origin: 5px 0px;
      transition: transform 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
            background 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
            opacity 0.55s ease;
    }
  }
}
</style>
