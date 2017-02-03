<template>
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
</template>

<script>
export default {
  name: 'fyi-nav',
  data () {
    return {
      tabs: ['All', 'Links', 'Media'],
      currentTab: 'All'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fyi-nav {
  margin: 15px 0;
}
</style>
