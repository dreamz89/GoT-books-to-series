<template>
  <div id="app">
    <div class="container">
      <sankey></sankey>
      <barcharts></barcharts>
    </div>
  </div>
</template>

<script>
import Sankey from './components/Sankey.vue'
import Barcharts from './components/Barcharts.vue'

export default {
  name: 'app',
  components: { Sankey, Barcharts }
}
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  .container {
    max-width: 1200px;
    margin: 0 auto;
  }
}
</style>
