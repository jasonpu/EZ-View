<template>
  <div class="fyi-embed">
    <div class="card">
      <fyi-card-context :origin="origin" v-if="origin.context && settings.context"></fyi-card-context>
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" :src="data.embed.url" v-if=" data.embed.type == 'iframe' ">
      </div>
      <div class="card-block">
        <fyi-card-title :data="data"></fyi-card-title>
        <fyi-card-actions type="embed" :origin="origin" :data="data" :settings="settings"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'
import FyiCardTitle from './FyiCardTitle'
import FyiCardContext from './FyiCardContext'

export default {
  name: 'fyi-embed',
  components: {
    FyiCardActions,
    FyiCardTitle,
    FyiCardContext
  },
  props: ['origin', 'data', 'settings']
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
