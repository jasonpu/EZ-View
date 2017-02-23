<template>
  <a :href="data.url" target="_blank" @click="open">
    <h4 class="card-title">{{ data.title }}</h4>
  </a>
</template>

<script>
export default {
  name: 'fyi-card-title',
  props: ['data'],
  methods: {
    open (event) {
      var self = this
      if (window.chrome && window.chrome.tabs) {
        event.preventDefault()
        window.chrome.tabs.create({
          url: self.data.url,
          active: false
        })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
