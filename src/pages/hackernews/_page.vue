<template>
  <div>
    <article>
      <ul>
        <li v-for="elem in result" :key="elem.id">
          <a :href="elem.url">{{ elem.title }} <span>({{ elem.domain }})</span></a>
          <p>{{ elem.points }} points by {{ elem.user }} {{ elem.time_ago }}</p>
        </li>
      </ul>
    </article>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  async asyncData ({ $axios, params, error }):Promise<Object> {
    const res = await $axios.$get(`https://api.hnpwa.com/v0/${params.page}/1.json`)
      .then((res: any) => {
        return res
      }).catch(() => {
        return error({ statusCode: 404 })
      })
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
