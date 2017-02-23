<template>
  <div class="fyi-card-actions">
    <div class="text-right">
      <a href="#" @click="bookmark" class="card-link" v-if="settings.services.bookmark">
        <i class="fa fa-bookmark fa-lg" aria-hidden="true"></i>
      </a>
      <a :href="twitter_url" target="_blank" class="card-link" v-if="settings.services.twitter">
        <i class="fa fa-twitter fa-lg" aria-hidden="true"></i>
      </a>
      <a :href="facebook_url" target="_blank" class="card-link" v-if="settings.services.facebook">
        <i class="fa fa-facebook-official fa-lg" aria-hidden="true"></i>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fyi-card-actions',
  props: ['url', 'settings'],
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
