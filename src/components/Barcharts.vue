<template>
  <div class="barcharts">
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
    <div class="season">
      <episode class="episode" :data="S1E1"></episode>
      <episode class="episode" :data="S1E2"></episode>
    </div>
  </div>
</template>

<script>
import S1E1 from '../data/GoT S1 E1.json'
import S1E2 from '../data/GoT S1 E2.json'
import episode from './Episode.vue'

export default {
  components: { episode },
  data () {
    return { S1E1, S1E2 }
  }
}
</script>

<style lang="scss">
.barcharts {
  max-width: 1200px;
  margin: 0 auto;

  .season {
    display: inline-block;
    height: 100%;
    width: calc(100% / 7);

    .episode {
      height: 200px;
      width: 50%;
      max-width: 50px;
      margin: 0 auto;
      cursor: pointer;
    }
  }
}
</style>
