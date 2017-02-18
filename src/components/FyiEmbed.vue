<template>
  <div class="fyi-embed">
    <div class="card">
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" :src="embed.url" v-if=" embed.type == 'iframe' ">
      </div>
      <div class="card-block">
        <a :href="data.url" target="_blank">
          <h4 class="card-title">{{ data.title }}</h4>
        </a>
        <fyi-card-actions :url="data.url"></fyi-card-actions>
      </div>
    </div>
  </div>
</template>

<script>
import FyiCardActions from './FyiCardActions'

export default {
  name: 'fyi-embed',
  components: {
    FyiCardActions
  },
  props: ['data', 'embed']
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
