<template>
  <div class="card-header d-flex flex-row">
    <i class="fa fa-quote-left align-self-start" aria-hidden="true"></i>
    <p class="col align-self-stretch">{{ origin.context }}</p>
    <i class="fa fa-quote-right align-self-end" aria-hidden="true"></i>
  </div>
</template>

<script>
export default {
  name: 'fyi-card-context',
  props: ['origin', 'settings']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  margin: 0;
}
</style>

