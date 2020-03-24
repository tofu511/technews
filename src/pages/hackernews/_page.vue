<template>
  <div>
    <pre>{{ result }}</pre>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  async asyncData (context):Promise<Object> {
    const res = await context.$axios.$get(`https://api.hnpwa.com/v0/${context.params.page}/1.json`)
    return { result: res }
  }
})

export default class Page extends Vue {
  // result: Object = {}
}
</script>
