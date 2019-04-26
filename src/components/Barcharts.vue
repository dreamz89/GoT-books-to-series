<template>
  <div class="barcharts">
    <div class="intro">
      <h1>Scene by scene comparison</h1>
      <p>
        Click on the barcharts below to see the scene by scene comparison of every episode and every season. The size of the scene is based on its duration proportionate to the whole episode.
      </p>
      <p>
        TRUE scenes are scenes that do happen in the books, albeit with some minor changes for the screen. MIXED scenes have elements that happen and elements that do not. FALSE are scenes that do not happen in the books at all. UNKNOWN are scenes that lack data (and time).
      </p>
    </div>
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
    <div class="seasons">
      <div class="season"
        ref="season"
        v-for="sn in 7"
        :key="sn">
        <div class="episodes">
          <p class="label">S{{ sn }}</p>
          <episode
            v-for="ep in 10"
            :key="ep"
            :data="data['S' + sn + 'E' + ep]"
            :season="sn"
            :episode="ep"
            :drilldown="drilldown"
            @chosen="drilldown = $event"
          ></episode>
        </div>
        <div class="description-wrap" v-show="sn === drilldown.season">
          <div class="inner-wrap" ref="innerWrap" :style="{ maxHeight: fullHeight() }">
            <div class="navigation">
              <img @click="up" src="nav-icon.svg"/>
              <img @click="down" src="nav-icon.svg"/>
            </div>
            <div class="content">
              <img src="close-icon.svg" @click="closeDescription" />
              <description
                :data="data['S' + drilldown.season + 'E' + drilldown.episode]"
                :drilldown="drilldown"
              ></description>
            </div>
          </div>
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
import S1E3 from '../data/GoT S1 E3.json'
import S1E4 from '../data/GoT S1 E4.json'
import S1E5 from '../data/GoT S1 E5.json'
import S1E6 from '../data/GoT S1 E6.json'
import S1E7 from '../data/GoT S1 E7.json'
import S1E8 from '../data/GoT S1 E8.json'
import S1E9 from '../data/GoT S1 E9.json'
import S1E10 from '../data/GoT S1 E10.json'
import S2E1 from '../data/GoT S2 E1.json'
import S2E2 from '../data/GoT S2 E2.json'
import S2E3 from '../data/GoT S2 E3.json'
import S2E4 from '../data/GoT S2 E4.json'
import S2E5 from '../data/GoT S2 E5.json'
import S2E6 from '../data/GoT S2 E6.json'
import S2E7 from '../data/GoT S2 E7.json'
import S2E8 from '../data/GoT S2 E8.json'
import S2E9 from '../data/GoT S2 E9.json'
import S2E10 from '../data/GoT S2 E10.json'
import S3E1 from '../data/GoT S3 E1.json'
import S3E2 from '../data/GoT S3 E2.json'
import S3E3 from '../data/GoT S3 E3.json'
import S3E4 from '../data/GoT S3 E4.json'
import S3E5 from '../data/GoT S3 E5.json'
import S3E6 from '../data/GoT S3 E6.json'
import S3E7 from '../data/GoT S3 E7.json'
import S3E8 from '../data/GoT S3 E8.json'
import S3E9 from '../data/GoT S3 E9.json'
import S3E10 from '../data/GoT S3 E10.json'
import S4E1 from '../data/GoT S4 E1.json'
import S4E2 from '../data/GoT S4 E2.json'
import S4E3 from '../data/GoT S4 E3.json'
import S4E4 from '../data/GoT S4 E4.json'
import S4E5 from '../data/GoT S4 E5.json'
import S4E6 from '../data/GoT S4 E6.json'
import S4E7 from '../data/GoT S4 E7.json'
import S4E8 from '../data/GoT S4 E8.json'
import S4E9 from '../data/GoT S4 E9.json'
import S4E10 from '../data/GoT S4 E10.json'
import S5E1 from '../data/GoT S5 E1.json'
import S5E2 from '../data/GoT S5 E2.json'
import S5E3 from '../data/GoT S5 E3.json'
import S5E4 from '../data/GoT S5 E4.json'
import S5E5 from '../data/GoT S5 E5.json'
import S5E6 from '../data/GoT S5 E6.json'
import S5E7 from '../data/GoT S5 E7.json'
import S5E8 from '../data/GoT S5 E8.json'
import S5E9 from '../data/GoT S5 E9.json'
import S5E10 from '../data/GoT S5 E10.json'
import S6E1 from '../data/GoT S6 E1.json'
import S6E2 from '../data/GoT S6 E2.json'
import S6E3 from '../data/GoT S6 E3.json'
import S6E4 from '../data/GoT S6 E4.json'
import S6E5 from '../data/GoT S6 E5.json'
import S6E6 from '../data/GoT S6 E6.json'
import S6E7 from '../data/GoT S6 E7.json'
import S6E8 from '../data/GoT S6 E8.json'
import S6E9 from '../data/GoT S6 E9.json'
import S6E10 from '../data/GoT S6 E10.json'
import S7E1 from '../data/GoT S7 E1.json'
import S7E2 from '../data/GoT S7 E2.json'
import S7E3 from '../data/GoT S7 E3.json'
import S7E4 from '../data/GoT S7 E4.json'
import S7E5 from '../data/GoT S7 E5.json'
import S7E6 from '../data/GoT S7 E6.json'
import S7E7 from '../data/GoT S7 E7.json'

export default {
  components: { episode, description },
  data () {
    return {
      fullData: {
        S1E1, S1E2, S1E3, S1E4, S1E5, S1E6, S1E7, S1E8, S1E9, S1E10,
        S2E1, S2E2, S2E3, S2E4, S2E5, S2E6, S2E7, S2E8, S2E9, S2E10,
        S3E1, S3E2, S3E3, S3E4, S3E5, S3E6, S3E7, S3E8, S3E9, S3E10,
        S4E1, S4E2, S4E3, S4E4, S4E5, S4E6, S4E7, S4E8, S4E9, S4E10,
        S5E1, S5E2, S5E3, S5E4, S5E5, S5E6, S5E7, S5E8, S5E9, S5E10,
        S6E1, S6E2, S6E3, S6E4, S6E5, S6E6, S6E7, S6E8, S6E9, S6E10,
        S7E1, S7E2, S7E3, S7E4, S7E5, S7E6, S7E7
      },
      data: {},
      drilldown: {
        season: 0,
        episode: 0,
        scene: 0
      },
      position: 0
    }
  },
  created () {
    Object.keys(this.fullData).forEach(episode => {
      this.data[episode] = this.fullData[episode].filter(scene => {
        return scene.Image !== null
      })
    })
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  watch: {
    drilldown () {
      if (this.drilldown.season !== 0) {
        this.$refs.season.forEach((season, i) => {
          if (i !== this.drilldown.season - 1) {
            season.classList.add('shrink')
          } else {
            season.classList.add('expand')
            if (this.position < 0) this.$refs.innerWrap[this.drilldown.season - 1].classList.add('fixed')
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
    },
    handleScroll () {
      const el = document.querySelector('.seasons')
      this.position = el.getBoundingClientRect().top

      if (this.drilldown.season !== 0) {
        if (this.position < 0) {
          this.$refs.innerWrap[this.drilldown.season - 1].classList.add('fixed')
        } else {
          this.$refs.innerWrap[this.drilldown.season - 1].classList.remove('fixed')
        }
      }
    },
    fullHeight () {
      return window.innerHeight + 'px'
    }
  }
}
</script>

<style lang="scss">
.barcharts {
  margin: 0 auto;
  overflow: hidden;

  .intro {
    max-width: 700px;
    margin: 0 auto;
    padding: 30px 15px;

    h1 {
      font-family: 'PT Sans', sans-serif;
      font-size: 30px;
      line-height: 1.3em;
      color: #E1EDF4;
      margin-bottom: 20px;
    }
    p {
      font-family: 'PT Sans', sans-serif;
      font-size: 15px;
      line-height: 1.3em;
      color: #E1EDF4;
    }
  }

  .indicator {
    text-align: center;

    > div {
      display: inline-block;
      margin: 0 10px;

      @media (max-width: 480px){
        margin: 0 5px;
      }

      > div {
        height: 15px;
        width: 15px;
        display: inline-block;
        vertical-align: middle;
      }

      > p {
        display: inline-block;
        margin-left: 10px;
        color: #E1EDF4;
        font-family: 'PT Sans', sans-serif;
        font-size: 15px;
        line-height: 1.3em;

        @media (max-width: 480px){
          margin-left: 5px;
        }
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

  .seasons {
    @media (max-width: 768px) {
      max-width: calc(100% - 27px);
      margin: 20px 0 20px 27px;
    }

    @media (min-width: 768px) {
      margin: 30px 15px;
    }

    .season {
      display: inline-block;
      height: 100%;
      width: calc(100% / 7);
      text-align: center;
      transition: width 0.5s ease;

      &.expand {
        width: 100%;

        @media (max-width: 768px) {
          margin-left: -5px;
        }

        .episodes {
          display: inline-block;
          width: calc(100% / 7);
        }

        .description-wrap {
          display: inline-block;
          width: calc(100% / 7 * 6 - 20px);
          opacity: 1;

          @media (max-width: 768px) {
            width: calc(100% / 7 * 6 - 10px);
          }
        }
      }

      &.shrink {
        width: 0;

        p {
          white-space: nowrap;
          visibility: hidden;
        }
      }

      .episodes {
        position: relative;

        .label {
          position: absolute;
          top: -24px;
          left: 50%;
          transform: translateX(-50%);
          margin: 0;
          font-family: 'PT Sans', sans-serif;
          font-size: 15px;
          line-height: 1.3em;
          color: #E1EDF4;
        }
      }

      .description-wrap {
        vertical-align: top;
        transition: width 0.5s ease;
        width: 0;
        opacity: 0;

        .inner-wrap {
          display: flex;
          flex-direction: row;

          &.fixed {
            position: fixed;
            top: 50%;
            transform: translateY(-50%);
            width: calc(100% / 7 * 6 - 45px);

            @media (min-width: 1000px) { // container width
              width: calc(1000px / 7 * 6 - 45px);
            }

            .content { // dont scroll the nav
              overflow-y: scroll;
            }
          }

          .navigation {
            display: flex;
            flex-direction: column;
            margin-top: 30px;

            img {
              margin: 0 5px 15px;
              width: 30px;
              transform: rotate(90deg);
              cursor: pointer;

              &:first-child {
                transform: rotate(-90deg);
              }

              @media (max-width: 480px) {
                width: 20px;
              }
            }
          }

          .content {
            margin: 0 auto;

            > img {
              height: 20px;
              float: right;
              margin-bottom: 10px;
              cursor: pointer;
            }
          }

          .description {
            clear:both
          }

          > p {
            font-size: 30px;
            cursor: pointer;
          }
        }
      }
    }
  }
}
</style>
