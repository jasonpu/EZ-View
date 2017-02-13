<template>
  <div class="fyi-article">
    <div class="row" v-if="data">
      <div class="col col-4">
        <a :href="data.url" target="_blank">
          <img v-if="data.lead_image_url" :src="data.lead_image_url" alt="">
        </a>
      </div>
      <div class="col col-8">
        <a :href="data.url" target="_blank">
          <h1>{{ data.title }}</h1>
        </a>
        <h2>
          {{ data.excerpt }}
        </h2>
      </div>
      <div class="col col-7">
      </div>
      <div class="col col-5">
        <button v-on:click="bookmark"><img src="~assets/bookmark.svg"></button>
        <button v-on:click="facebook"><img src="~assets/facebook.svg"></button>
        <button v-on:click="twitter"><img src="~assets/twitter.svg"></button>
        <button v-on:click="more"><img src="~assets/more.svg"></button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'fyi-article',
  data () {
    return {
      url: '',
      data: null
    }
  },
  created () {
    this.fetchURL()
  },
  watch: {
    url () {
      if (this.url) {
        // TODO: need to filter out chrome:// and other weird link
        this.fetchData()
      }
    }
  },
  methods: {
    fetchURL () {
      var self = this
      if (window.chrome && window.chrome.tabs) {
        window.chrome.tabs.query({
          active: true,
          currentWindow: true
        }, function (tabs) {
          var tab = tabs[0]
          var url = tab.url
          console.assert(typeof url === 'string', 'tab.url should be a string')

          self.url = url
        })
      } else if (window.safari && window.safari.application) {
        self.url = window.safari.application.activeBrowserWindow.activeTab.url
      } else {
        // use dummy for easy dev
        this.url = 'https://www.nytimes.com/2017/02/02/world/middleeast/iran-missile-test-trump.html'
      }
    },
    fetchData () {
      var self = this
      if (!this.data) {
        axios.get('https://mercury.postlight.com/parser?url=' + this.url, {
          headers: {
            'x-api-key': '8CwzdCirC38J5RgE4gVQGym2YFxEVgn92nIHjxnd'
          }
        })
        .then(function (response) {
          self.data = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    },
    bookmark () {
      // add url to local bookmark storage
    },
    facebook () {
      // share to facebook
    },
    twitter () {
      // share to twitter
    },
    more () {
      // view more
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fyi-article {
  margin-bottom: 1em;
}
img {
  max-width: 100%;
  text-align: center;
}
h1, h2 {
  font-weight: normal;
}
h1 {
  font-weight: bold;
  margin: 0;
  font-size: 20px;
  line-height: 1.1;
  display: block;
  margin-bottom: 4px;
  color: #212325;
  position: relative
}
h2 {
  line-height: 1.3;
  font-size: 16px;
  margin: 0;
  color: #7a7c7e;
  display: block
}
a {
  color: #42b983;
}

button {
  border: none;
  width: 2em;
  padding: 0em;
  background: #fff;
  margin-right: 0.5em;
  cursor: pointer;
}
button:last-child {
  margin-right: 0;
}
</style>
