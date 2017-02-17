<template>
  <div class="fyi-card-actions">
    <div class="text-right">
      <a href="#" @click="bookmark" class="card-link"><i class="fa fa-bookmark fa-lg" aria-hidden="true"></i></a>
      <a :href="facebook_url" target="_blank" class="card-link"><i class="fa fa-facebook-official fa-lg" aria-hidden="true"></i></a>
      <a :href="twitter_url" target="_blank" class="card-link"><i class="fa fa-twitter fa-lg" aria-hidden="true"></i></a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fyi-embed',
  props: ['url'],
  computed: {
    facebook_url () {
      return 'http://facebook.com/sharer.php?u=' + encodeURIComponent(this.url)
    },
    twitter_url () {
      return 'https://twitter.com/intent/tweet?url=' + encodeURIComponent(this.url)
    }
  },
  methods: {
    bookmark () {
      // TODO: bookmark
      window.alert('TODO: bookmark ' + this.url)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
