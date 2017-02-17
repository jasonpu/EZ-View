<template>
  <div class="fyi-article">
    <div class="card">
      <img class="card-img-top" :src="data.lead_image_url" alt="" v-if="data.lead_image_url">
      <div class="card-block">
        <a :href="data.url" target="_blank">
          <h4 class="card-title">{{ data.title }}</h4>
        </a>
        <p class="card-text">{{ data.excerpt }}</p>
      </div>
      <div class="card-block text-right">
        <a href="#" @click="bookmark" class="card-link"><i class="fa fa-lg fa-bookmark" aria-hidden="true"></i></a>
        <a :href="facebook_url" target="_blank" class="card-link"><i class="fa fa-lg fa-facebook-official" aria-hidden="true"></i></a>
        <a :href="twitter_url" target="_blank" class="card-link"><i class="fa fa-lg fa-twitter" aria-hidden="true"></i></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fyi-article',
  props: ['data'],
  computed: {
    facebook_url () {
      return 'http://facebook.com/sharer.php?u=' + encodeURIComponent(this.data.url)
    },
    twitter_url () {
      return 'https://twitter.com/intent/tweet?url=' + encodeURIComponent(this.data.url)
    }
  },
  methods: {
    bookmark () {
      // TODO: bookmark
      window.alert('TODO: bookmark')
    }
  }
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
