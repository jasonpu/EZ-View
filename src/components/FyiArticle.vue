<template>
  <div class="fyi-article">
    <div class="card">
      <fyi-card-context :origin="origin" v-if="origin.context && settings.context"></fyi-card-context>
      <img :class="{ 'card-img-top': !(origin.context && settings.context) }" :src="data.lead_image_url" alt="" v-if="data.lead_image_url">
      <div class="card-block">
        <fyi-card-title :data="data"></fyi-card-title>
        <p class="card-text">{{ data.excerpt }}</p>
        <fyi-card-actions type="article" :origin="origin" :data="data" :settings="settings"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'
import FyiCardTitle from './FyiCardTitle'
import FyiCardContext from './FyiCardContext'

export default {
  name: 'fyi-article',
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
.fyi-article {
  margin-bottom: 1em;
}
img {
  max-width: 100%;
}
</style>
