<template>
  <div id="app">
    <div class="container">
      <div class="fyi-nav clearfix">
        <ul class="nav nav-pills float-left">
          <li class="nav-item" v-for="tab in tabs">
            <a class="nav-link" href="#" v-bind:class="{ active: tab === currentTab }"
                                        v-on:click="currentTab = tab">{{ tab }}</a>
          </li>
        </ul>
        <ul class="nav float-right">
          <li class="nav-item">
            <a class="nav-link" href="#">Settings</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="container-fluid">
      <fyi-cards :filter="currentTab"></fyi-cards>
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
      tabs: ['All', 'Links', 'Media'],
      currentTab: 'All'
    }
  }
}
</script>

<style>
#app {
  width: 30em;
}
.fyi-nav {
  margin: 1em 0;
}
</style>
