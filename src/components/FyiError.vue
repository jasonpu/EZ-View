<template>
  <div class="fyi-message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'fyi-message',
  props: ['message']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
