<template>
  <div class="barcharts">
    <episode class="episode" :data="S1E1"></episode>

  </div>
</template>

<script>
import S1E1 from '../../data/GoT S1 E1.json'
import episode from './Episode.vue'

export default {
  components: { episode },
  data () {
    return {
      S1E1
    }
  }
}

</script>

<style lang="scss">
.barcharts {
  max-width: 1200px;

  .episode {
    height: 200px;
    width: 30px;
  }
}
</style>
