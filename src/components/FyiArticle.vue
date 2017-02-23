<template>
  <div class="fyi-article">
    <div class="card">
      <img class="card-img-top" :src="data.lead_image_url" alt="" v-if="data.lead_image_url">
      <div class="card-block">
        <fyi-card-title :data="data"></fyi-card-title>
        <p class="card-text">{{ data.excerpt }}</p>
        <fyi-card-actions :url="data.url" :settings="settings"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'
import FyiCardTitle from './FyiCardTitle'

export default {
  name: 'fyi-article',
  components: {
    FyiCardActions,
    FyiCardTitle
  },
  props: ['data', 'settings']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fyi-article {
  margin-bottom: 1em;
}
img {
  max-width: 100%;
}
</style>
