<template>
  <div class="fyi-card">
    <fyi-error   :data="data" :settings="settings" v-if=" type == 'error' "></fyi-error>
    <fyi-article :origin="origin" :data="data" :settings="settings" v-else-if=" type == 'article' "></fyi-article>
    <fyi-embed   :origin="origin" :data="data" :settings="settings" v-else-if=" type == 'embed' "></fyi-embed>
  </div>
</template>

<script>
import FyiError from './FyiError'
import FyiArticle from './FyiArticle'
import FyiEmbed from './FyiEmbed'

export default {
  name: 'fyi-card',
  components: {
    FyiError,
    FyiArticle,
    FyiEmbed
  },
  props: ['origin', 'data', 'type', 'settings']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fyi-card {
  margin-bottom: 1em;
}
</style>
