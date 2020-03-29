<template>
  <div>
    <pre>{{ result }}</pre>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  async asyncData ({ $axios, params }):Promise<Object> {
    const res = await $axios.$get(`https://api.hnpwa.com/v0/${params.page}/1.json`)
    return { result: res }
  }
})

export default class Page extends Vue {}
</script>
