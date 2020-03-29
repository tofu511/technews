<template>
  <div>
    <pre>
      {{ result }}
    </pre>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

const routing = (path: string): string => {
  const pair = {
    rising: 'articles?state=rising',
    week: 'articles?top=7',
    month: 'articles?top=30',
    year: 'articles?top=365',
    podcast: 'podcast_episodes'
  }
  const res = pair[path]
  return res || ''
}

@Component({
  async asyncData ({ $axios, params }):Promise<Object> {
    const res = await $axios.$get(`https://dev.to/api/${routing(params.page)}`)
    return { result: res }
  }
})

export default class Page extends Vue {}

</script>
