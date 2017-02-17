<template>
  <div class="fyi-article">
    <div class="row">
      <div class="col">
        <a :href="data.url" target="_blank">
          <h1>{{ data.title }}</h1>
        </a>
      </div>
    </div>
    <div class="row" v-if="data.lead_image_url">
      <div class="col col-4">
        <a :href="data.url" target="_blank">
          <img :src="data.lead_image_url" alt="">
        </a>
      </div>
      <div class="col col-8">
        <h2>
          {{ data.excerpt }}
        </h2>
      </div>
    </div>
    <div class="row" v-else>
      <div class="col">
        <h2>
          {{ data.excerpt }}
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fyi-article',
  props: ['data']
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
