<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  fetch ({ redirect }) {
    redirect(301, '/hackernews/news')
  }
})

export default class Page extends Vue {}
</script>
