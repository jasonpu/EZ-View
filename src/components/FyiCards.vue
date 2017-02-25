<template>
  <div class="fyi-cards">
    <div class="progress" v-if="progress">
      <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%"></div>
    </div>
    <transition-group name="list">
      <fyi-card :key="item" :origin="item.origin" :data="item.data" :type="item.type" :settings="settings" v-for="item in filter()"></fyi-card>
    </transition-group>
  </div>
</template>

<script>
import axios from 'axios'
import getVideoID from 'get-video-id'
import FyiCard from './FyiCard'

export default {
  name: 'fyi-cards',
  components: {
    FyiCard
  },
  props: ['settings'],
  data () {
    return {
      items: [],
      progress: true
    }
  },
  created () {
    this.fetchActiveTabURL(function (url) {
      this.fetchData(url, null, function (data) {
        this.progress = false

        if (data == null || data.error) {
          this.items.push({
            type: 'error',
            origin: null,
            data: {
              message: 'Sorry, we cannot load content from this page.'
            }
          })
        } else {
          this.fetchAll(data)
        }
      })
    })
  },
  methods: {
    filter () {
      var self = this
      return this.items.filter(function (item) {
        if (item.data != null && item.type != null) {
          if (self.settings.filter === 'all') {
            return true
          } else if (self.settings.filter === 'article' && item.type === 'article') {
            return true
          } else if (self.settings.filter === 'embed' && item.type === 'embed') {
            return true
          }
        }
        return false
      })
    },
    fetchActiveTabURL (callback) {
      var self = this
      var url
      if (window.chrome && window.chrome.tabs) {
        window.chrome.tabs.query({
          active: true,
          currentWindow: true
        }, function (tabs) {
          var tab = tabs[0]
          url = tab.url
          console.assert(typeof url === 'string', 'tab.url should be a string')

          callback.call(self, url)
        })
      } else if (window.safari && window.safari.application) {
        url = window.safari.application.activeBrowserWindow.activeTab.url
        callback.call(self, url)
      } else {
        url = 'http://kotaku.com/a-17-hour-video-of-a-guy-clicking-his-mouse-one-million-1792454584'
        callback.call(self, url)
      }
    },
    fetchData (url, context, callback) {
      var self = this
      for (var i = 0; i < this.items.length; ++i) {
        if (this.items[i].origin.url === url || (this.items[i].data && this.items[i].data === url)) {
          return
        }
      }
      this.items.push({
        origin: {
          url: url,
          context: context
        }
      })
      axios.get('https://mercury.postlight.com/parser?url=' + encodeURIComponent(url), {
        headers: {
          'x-api-key': '8CwzdCirC38J5RgE4gVQGym2YFxEVgn92nIHjxnd'
        }
      })
      .then(function (response) {
        (function () {
          var data = response.data

          if (data != null && !data.error) {
            data.url = new window.URL(data.url, url).href // normalize broken URLs

            for (var i = 0; i < this.items.length; ++i) {
              if (this.items[i].data && this.items[i].data.url === data.url) {
                return
              } else if (this.items[i].origin.url === url) {
                var video

                if ((video = getVideoID(data.url)) != null && video.id != null) {
                  switch (video.service) {
                    case 'youtube':
                      data.embed = {
                        url: 'https://www.youtube.com/embed/' + video.id,
                        type: 'iframe'
                      }
                      break
                    case 'vimeo':
                      data.embed = {
                        url: 'https://player.vimeo.com/video/' + video.id,
                        type: 'iframe'
                      }
                      break
                    case 'vine':
                      data.embed = {
                        url: 'https://vine.co/v/' + video.id + '/embed/simple',
                        type: 'iframe'
                      }
                      break
                    case 'videopress':
                      data.embed = {
                        url: 'https://videopress.com/embed/' + video.id,
                        type: 'iframe'
                      }
                      break
                  }
                  this.items.splice(i, 1, {
                    type: 'embed',
                    origin: this.items[i].origin,
                    data: data
                  })
                } else {
                  this.items.splice(i, 1, {
                    type: 'article',
                    origin: this.items[i].origin,
                    data: data
                  })
                }
              }
            }
          }
          if (callback) {
            callback.call(this, data)
          }
        }).call(self)
      })
      .catch(function (error) {
        console.log(error)
      })
    },
    fetchAll (data, callback) {
      var dom = document.createElement('div')
      dom.innerHTML = data.content
      var anchors = dom.querySelectorAll('a[href]')
      for (var i = 0; i < anchors.length; ++i) {
        var url = new window.URL(anchors[i].href, data.url)
        if (/^https?:$/.test(url.protocol)) {
          url.hash = ''
          this.fetchData(url.href, anchors[i].textContent)
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.progress {
  margin-bottom: 1em;
}
.list-item {
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
}
</style>
