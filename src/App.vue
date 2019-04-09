<template>
  <div id="app">
    <div class="container">
      <intro></intro>
      <sankey></sankey>
      <barcharts></barcharts>
    </div>
  </div>
</template>

<script>
import Intro from './components/Intro.vue'
import Sankey from './components/Sankey.vue'
import Barcharts from './components/Barcharts.vue'

export default {
  name: 'app',
  components: { Intro, Sankey, Barcharts }
}
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  background-color: #101729;

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }
}
</style>
