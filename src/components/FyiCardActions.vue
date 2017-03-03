<template>
  <div class="fyi-card-actions">
    <div class="text-right">
      <a href="#" @click.prevent="pin" class="card-link" v-if="settings.services.bookmark">
        <i class="fa fa-lg" :class="pinned_icon" aria-hidden="true"></i>
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
  props: ['data', 'origin', 'type', 'settings'],
  data () {
    var self = this
    return {
      isPinned: (function () {
        try {
          var pinned = JSON.parse(window.localStorage.getItem('pinned'))
          if (pinned != null) {
            for (var i = 0; i < pinned.length; i++) {
              if (pinned[i].data.url === self.data.url) {
                return true
              }
            }
          }
        } catch (err) {}
        return false
      })()
    }
  },
  computed: {
    pinned_icon () {
      return this.isPinned ? 'fa-bookmark' : 'fa-bookmark-o'
    },
    facebook_url () {
      return 'http://facebook.com/sharer.php?u=' + encodeURIComponent(this.data.url)
    },
    twitter_url () {
      return 'https://twitter.com/intent/tweet?url=' + encodeURIComponent(this.data.url)
    }
  },
  methods: {
    pin () {
      var self = this
      var pinned
      try {
        pinned = JSON.parse(window.localStorage.getItem('pinned'))
        if (pinned != null) {
          for (var i in pinned) {
            if (pinned[i].data.url === this.data.url) {
              pinned.splice(i, 1)
              window.localStorage.setItem('pinned', JSON.stringify(pinned))
              self.isPinned = false
              return
            }
          }
        }
      } catch (err) {}
      if (pinned == null) {
        pinned = []
      }
      pinned.push({
        type: self.type,
        origin: self.origin,
        data: self.data
      })
      window.localStorage.setItem('pinned', JSON.stringify(pinned))
      self.isPinned = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
