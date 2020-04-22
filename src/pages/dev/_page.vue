<template>
  <div>
    <article>
      <ul>
        <li v-for="elem in result" :key="elem.id">
          <a :href="elem.url">{{ elem.title }} </a>
          <p>{{ elem.description }}</p>
          <p>created by {{ elem.user.name }} a.k.a. {{ elem.user.username }}</p>
        </li>
      </ul>
    </article>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

interface LinkPair {
  [key: string]: string;
}

const routing = (path: string): string => {
  const pair = {
    rising: 'articles?state=rising',
    week: 'articles?top=7',
    month: 'articles?top=30',
    year: 'articles?top=365'
  } as LinkPair
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

<style lang="scss" scoped>
li {
  list-style: decimal;
  margin-top: 21px;
  margin-bottom: 21px;

  a {
    text-decoration: none;
    color: #212121;

    span {
      font-size: 16px;
      color: #828282;
    }
  }
  p {
    font-size: 16px;
    color: #828282;
  }
}
</style>
