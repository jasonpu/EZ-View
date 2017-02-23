<template>
  <div class="fyi-article">
    <div class="card">
      <img class="card-img-top" :src="data.lead_image_url" alt="" v-if="data.lead_image_url">
      <div class="card-block">
        <a :href="data.url" target="_blank">
          <h4 class="card-title">{{ data.title }}</h4>
        </a>
        <p class="card-text">{{ data.excerpt }}</p>
        <fyi-card-actions :url="data.url" :settings="settings"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'

export default {
  name: 'fyi-article',
  components: {
    FyiCardActions
  },
  props: ['data', 'settings']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fyi-article {
  margin-bottom: 1em;
}
.card-title-link {
  color: inherit;
}
img {
  max-width: 100%;
}
</style>
