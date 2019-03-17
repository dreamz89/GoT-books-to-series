<template>
  <div id="app">
    <sankey></sankey>
    <barcharts></barcharts>
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

<style>
body {
  margin: 0;
}
#app {
}
</style>
