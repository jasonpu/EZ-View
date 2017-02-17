<template>
  <div class="fyi-cards">
    <div class="fyi-card" v-for="item in items">
      <fyi-error :message="item.message" v-if=" item.type == 'error' "></fyi-error>
      <fyi-article :data="item.data" v-else-if=" item.type == 'article' && item.data "></fyi-article>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import FyiError from './FyiError'
import FyiArticle from './FyiArticle'

export default {
  name: 'fyi-cards',
  components: {
    FyiError,
    FyiArticle
  },
  data () {
    return {
      items: []
    }
  },
  created () {
    this.fetchActiveTabURL(function (url) {
      this.fetchData(url, function (data) {
        if (data == null || data.error) {
          this.items.push({
            type: 'error',
            message: 'Sorry, we cannot load content from this page.'
          })
        } else {
          this.items.push({
            type: 'article',
            data: data
          })
          this.fetchAll(data)
        }
      })
    })
  },
  methods: {
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
        url = 'http://www.latimes.com/politics/la-na-pol-trump-news-conference-20170216-story.html'
        callback.call(self, url)
      }
    },
    fetchData (url, callback) {
      var self = this
      if (!this.data) {
        axios.get('https://mercury.postlight.com/parser?url=' + url, {
          headers: {
            'x-api-key': '8CwzdCirC38J5RgE4gVQGym2YFxEVgn92nIHjxnd'
          }
        })
        .then(function (response) {
          if (callback) {
            callback.call(self, response.data)
          }
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    },
    fetchAll (data, callback) {
      var dom = document.createElement('div')
      dom.innerHTML = data.content
      var anchors = dom.querySelectorAll('a[href]')
      for (var i = 0; i < anchors.length; ++i) {
        var url = new window.URL(anchors[i].href, data.url)
        if (/^https?:$/.test(url.protocol)) {
          url.hash = ''
          if (url.href !== data.url) {
            this.fetchData(url.href, function (data) {
              if (data) {
                this.items.push({
                  type: 'article',
                  data: data
                })
              }
            })
          }
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
