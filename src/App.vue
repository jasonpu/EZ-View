<template>
  <div id="app">
    <div class="container-fluid">
      <fyi-config></fyi-config>
    </div>
    <div class="container">
      <fyi-nav></fyi-nav>
    </div>
    <div class="container-fluid">
      <fyi-article></fyi-article>
    </div>
  </div>
</template>

<script>
// import Config from './components/Hello'
import FyiConfig from './components/FyiConfig'
import FyiNav from './components/FyiNav'
import FyiArticle from './components/FyiArticle'

export default {
  name: 'app',
  components: {
    FyiConfig,
    FyiNav,
    FyiArticle
  }
}
</script>

<style>
#app {
  width: 30em;
}
</style>
