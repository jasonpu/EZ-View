<template>
  <div class="fyi-error">
    <div class="card card-outline-danger">
      <div class="card-block">
        <blockquote class="card-blockquote">
          <p>{{ message }}</p>
        </blockquote>
      </div>
    </div>
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
