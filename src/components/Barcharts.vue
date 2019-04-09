<template>
  <div class="barcharts">
    <div class="indicator">
      <div>
        <div></div>
        <p>True</p>
      </div>
      <div>
        <div></div>
        <p>False</p>
      </div>
      <div>
        <div></div>
        <p>Mixed</p>
      </div>
      <div>
        <div></div>
        <p>Unknown</p>
      </div>
    </div>
    <div class="season"
      ref="season"
      v-for="sn in 7"
      :key="sn">
      <episode
        class="episode"
        v-for="ep in 2"
        :key="ep"
        :data="data['S' + sn + 'E' + ep]"
        :season="sn"
        :episode="ep"
        :drilldown="drilldown"
        @chosen="drilldown = $event"
      ></episode>
      <div class="description-wrap" v-show="sn === drilldown.season">
        <div class="inner-wrap">
          <div class="navigation">
            <div @click="up">&#11014;</div>
            <div @click="down">&#11015;</div>
          </div>
          <description
            :data="data['S' + drilldown.season + 'E' + drilldown.episode]"
            :drilldown="drilldown"
          ></description>
          <p @click="closeDescription">X</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import episode from './Episode.vue'
import description from './Description.vue'
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

export default {
  components: { episode, description },
  data () {
    return {
      fullData: {
        S1E1, S1E2,
        S2E1, S2E2,
        S3E1, S3E2,
        S4E1, S4E2,
        S5E1, S5E2,
        S6E1, S6E2,
        S7E1, S7E2
      },
      data: {},
      drilldown: {
        season: 0,
        episode: 0,
        scene: 0
      }
    }
  },
  created () {
    Object.keys(this.fullData).forEach(episode => {
      this.data[episode] = this.fullData[episode].filter(scene => {
        return scene.Image !== null
      })
    })
  },
  watch: {
    drilldown () {
      if (this.drilldown.season !== 0) {
        this.$refs.season.forEach((season, i) => {
          if (i !== this.drilldown.season - 1) {
            season.classList.add('shrink')
          } else {
            season.classList.add('expand')
          }
        })
      }
    }
  },
  methods: {
    closeDescription () {
      this.drilldown = {
        season: 0,
        episode: 0,
        scene: 0
      }
      this.$refs.season.forEach(season => {
        season.classList.remove('expand')
        season.classList.remove('shrink')
      })
    },
    up () {
      if (this.drilldown.scene > 1) {
        this.drilldown.scene -= 1
      } else {
        this.drilldown.scene = this.data['S' + this.drilldown.season + 'E' + this.drilldown.episode].length
        this.drilldown.episode -= 1
      }
    },
    down () {
      if (this.drilldown.scene < this.data['S' + this.drilldown.season + 'E' + this.drilldown.episode].length) {
        this.drilldown.scene += 1
      } else {
        this.drilldown.scene = 1
        this.drilldown.episode += 1
      }
    }
  }
}
</script>

<style lang="scss">
.barcharts {
  margin: 0 auto;
  overflow: hidden;

  .indicator {
    text-align: center;

    > div {
      display: inline-block;
      margin: 0 10px;

      > div {
        height: 15px;
        width: 15px;
        display: inline-block;
        vertical-align: middle;
      }

      > p {
        display: inline-block;
        margin-left: 10px;
        color: white;
        font-family: 'PT Sans', sans-serif;
        font-size: 15px;
        line-height: 1.3em;
      }
    }

    > div:nth-child(1) {
      > div {
        background-color: #404E86;
      }
    }
    > div:nth-child(2) {
      > div {
        background-color: #B23E4D;
      }
    }
    > div:nth-child(3) {
      > div {
        background-color: #7994C3;
      }
    }
    > div:nth-child(4) {
      > div {
        background-color: #C0CAC9;
      }
    }
  }

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

      .description-wrap {
        display: inline-block;
        width: calc(100% / 7 * 6);
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

    .episode {
      height: 200px;
      width: 50%;
      max-width: 50px;
      margin: 0 auto;
      cursor: pointer;
    }

    .description-wrap {
      display: inline-block;
      vertical-align: text-top;
      transition: width 0.5s ease;
      width: 0;
      opacity: 0;

      .inner-wrap {
        display: flex;
        flex-direction: row;

        .navigation {
          display: flex;
          flex-direction: column;
          justify-content: center;

          div {
            margin: 10px 5px;
            font-size: 28px;
            cursor: pointer;
          }
        }

        > p {
          font-size: 30px;
          cursor: pointer;
        }
      }
    }
  }
}
</style>
