<template>
  <div class="fyi-embed">
    <div class="card">
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" :src="data.embed.url" v-if=" data.embed.type == 'iframe' ">
      </div>
      <div class="card-block">
        <fyi-card-title :data="data"></fyi-card-title>
        <fyi-card-actions :url="data.url" :settings="settings"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'
import FyiCardTitle from './FyiCardTitle'

export default {
  name: 'fyi-embed',
  components: {
    FyiCardActions,
    FyiCardTitle
  },
  props: ['data', 'settings']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card-title-link {
  color: inherit;
}
img {
  max-width: 100%;
}
</style>
