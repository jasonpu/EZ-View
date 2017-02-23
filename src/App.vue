<template>
  <div id="app">
    <div class="container">
      <div class="fyi-nav clearfix">
        <ul class="nav nav-pills float-left">
          <li class="nav-item" v-for="tab in tabs">
            <a class="nav-link" href="#" tabindex="-1" :class="{ active: tab == settings.filter }"
                                         @click="settings.filter = tab">{{ tab }}</a>
          </li>
        </ul>
        <ul class="nav nav-pills float-right">
          <li class="nav-item">
            <a class="nav-link" href="#" tabindex="-1" :class="{ active: showSettings == true }"
                                         @click="showSettings = !showSettings">Settings</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="fyi-settings">
      <transition name="fade">
        <div class="inset-shadow-top" v-if="showSettings"></div>
      </transition>
      <transition name="slide-down">
        <div class="inset-shadow-bottom" v-if="showSettings">
          <div class="container">
            <form>
              <fieldset class="form-group">
                <legend>Sharing</legend>
                <div class="form-check">
                  <label class="form-check-label">
                    <input class="form-check-input" type="checkbox" v-model="settings.sharing.bookmark">
                    Bookmark
                  </label>
                </div>
                <div class="form-check">
                  <label class="form-check-label">
                    <input class="form-check-input" type="checkbox" v-model="settings.sharing.twitter">
                    Twitter
                  </label>
                </div>
                <div class="form-check">
                  <label class="form-check-label">
                    <input class="form-check-input" type="checkbox" v-model="settings.sharing.facebook">
                    Facebook
                  </label>
                </div>
              </fieldset>
            </form>
          </div>
        </div>
      </transition>
    </div>
    <div class="container-fluid">
      <fyi-cards :settings="settings"></fyi-cards>
    </div>
  </div>
</template>

<script>
import FyiCards from './components/FyiCards'

export default {
  name: 'app',
  components: {
    FyiCards
  },
  data () {
    return {
      settings: (function () {
        try {
          var settings = JSON.parse(window.localStorage.getItem('settings'))
          if (settings != null) {
            return settings
          }
        } catch (err) {}
        return {
          filter: 'All',
          sharing: {
            bookmark: true,
            twitter: true,
            facebook: true
          }
        }
      })(),
      tabs: ['All', 'Links', 'Media'],
      showSettings: false
    }
  },
  watch: {
    settings: {
      handler: function () {
        window.localStorage.setItem('settings', JSON.stringify(this.settings))
      },
      deep: true
    }
  }
}
</script>

<style>
#app {
  width: 30em;
}
.fyi-nav {
  margin-top: 1em;
  margin-bottom: 1em;
  background: #fff;
}
.fyi-settings {
  overflow: hidden;
}
.fyi-settings .container {
  padding-top: 1em;
  padding-bottom: 1em;
  margin-bottom: 1em;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
.inset-shadow-top {
  box-shadow: inset 0  6px 6px -8px #333;
  height: 6px;
}
.inset-shadow-bottom {
  box-shadow: inset 0 -6px 6px -8px #333;
}
.slide-down-enter-active, .slide-down-leave-active {
  transition: margin-top .5s;
}
.slide-down-enter-active {
  transition-timing-function: ease-out;
}
.slide-down-leave-active {
  transition-timing-function: ease-in;
}
.slide-down-enter, .slide-down-leave-to /* .slide-down-leave-active in <2.1.8 */ {
  margin-top: -200px; /* must be a number larger than height */
}
</style>
