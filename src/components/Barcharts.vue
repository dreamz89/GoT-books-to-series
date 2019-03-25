<template>
  <div class="barcharts">
    <div class="season"
      ref="season"
      v-for="sn in 7"
      :key="sn">
      <div class="indicator">
        <p>SEASON {{ sn }}</p>
        <episode
          class="episode"
          v-for="ep in 2"
          :key="ep"
          :data="data['S' + sn + 'E' + ep]"
          :season="sn"
          :episode="ep"
          @expand="showDetails = $event"
        ></episode>
      </div>
      <div class="description" v-if="sn === showDetails.season">
        <img src="../images/season 01/GoT 01 01 01.jpg"/>
      </div>
    </div>
  </div>
</template>

<script>
import S1E1 from '../data/GoT S1 E1.json'
import S1E2 from '../data/GoT S1 E2.json'
import S2E1 from '../data/GoT S1 E1.json'
import S2E2 from '../data/GoT S1 E2.json'
import S3E1 from '../data/GoT S1 E1.json'
import S3E2 from '../data/GoT S1 E2.json'
import S4E1 from '../data/GoT S1 E1.json'
import S4E2 from '../data/GoT S1 E2.json'
import S5E1 from '../data/GoT S1 E1.json'
import S5E2 from '../data/GoT S1 E2.json'
import S6E1 from '../data/GoT S1 E1.json'
import S6E2 from '../data/GoT S1 E2.json'
import S7E1 from '../data/GoT S1 E1.json'
import S7E2 from '../data/GoT S1 E2.json'
import episode from './Episode.vue'

export default {
  components: { episode },
  data () {
    return {
      data: {
        S1E1, S1E2,
        S2E1, S2E2,
        S3E1, S3E2,
        S4E1, S4E2,
        S5E1, S5E2,
        S6E1, S6E2,
        S7E1, S7E2
      },
      showDetails: {
      season: 0}
    }
  },
  watch: {
    showDetails () {
      this.$refs.season.forEach((season, i) => {
        if (i !== this.showDetails.season - 1) {
          season.classList.add('shrink')
        } else {
          season.classList.add('expand')
        }
      })
    }
  }
}
</script>

<style lang="scss">
.barcharts {
  margin: 0 auto;
  overflow: hidden;

  .season {
    display: inline-block;
    height: 100%;
    width: calc(100% / 7);
    text-align: center;
    transition: width 0.5s ease;

    &.expand {
      width: 100%;

      .indicator {
        display: inline-block;
        width: calc(100% / 7);
      }

      .description {
        display: inline-block;
        width: 70%;
        opacity: 1;
      }
    }

    &.shrink {
      width: 0;

      p {
        white-space: nowrap;
        visibility: hidden;
      }
    }

    .indicator {

      .episode {
        height: 200px;
        width: 50%;
        max-width: 50px;
        margin: 0 auto;
        cursor: pointer;
      }
    }

    .description {
      display: inline-block;
      vertical-align: text-top;
      transition: width 2s ease;
      width: 0;
      opacity: 0;
    }
  }
}
</style>
