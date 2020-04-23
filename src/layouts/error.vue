<template>
  <div class="error-container">
    <div v-if="error.statusCode == 404" class="error">
      404 Not Found 😢
    </div>
    <div v-else class="error">
      500 Internal Server Error 😢
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    error: {
      type: Object,
      required: false,
      default: null
    }
  }
})
</script>
<style lang="scss" scoped>
.error-container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #fff;
}

.error {
  font-size: 24px;
}
</style>
