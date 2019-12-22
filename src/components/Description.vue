<template>
  <div class="description">
    <div class="details">
      <div>
        <p class="title">{{ sceneData.Scene }}</p>
        <p class="ep-name">
          EPISODE {{ drilldown.episode }}: {{ EpisodeNames[drilldown.season][drilldown.episode]}}
        </p>
      </div>
      <div>
        <p class="rating" :style="{ backgroundColor: color }">{{ sceneData.Rating }}</p>
      </div>
    </div>
    <img :src="'images/season' + drilldown.season + '/GoT ' + drilldown.season + ' ' + drilldown.episode + ' '  + drilldown.scene + imageSize()" alt="screenshot of scene"/>
    <p class="comparison" v-html="sceneData.Comparison"></p>
  </div>
</template>

<script>
import EpisodeNames from '../data/EpisodeNames.json'

export default {
  props: ['data', 'drilldown'],
  data () {
    return {
      color: null,
      sceneData: {},
      EpisodeNames
    }
  },
  watch: {
    drilldown: {
      handler: function () {
        this.updateData()
      },
      deep: true,
      immediate: true
    }
  },
  methods: {
    updateData () {
      if (this.drilldown.season !== 0) {
        this.sceneData = this.data.filter(scene => {
          return scene.Image === this.drilldown.scene
        })[0]

        if (this.sceneData.Rating === 'TRUE') {
          this.color = '#404E86'
        } else if (this.sceneData.Rating === 'FALSE'){
          this.color = '#B23E4D'
        } else if (this.sceneData.Rating === 'MIXED'){
          this.color = '#7994C3'
        } else {
          this.color = '#C0CAC9'
        }
      }
    },
    imageSize () {
      return window.innerWidth > 420 ? '.jpg' : ' mobile.jpg'
    }
  }
}
</script>

<style lang="scss">
.description {
  width: 100%;

  .details {
    display: flex;
    max-width: 640px;
    margin: 0 auto;
    justify-content: space-between;

    > div {

      .title {
        font-family: 'PT Sans', sans-serif;
        font-size: 20px;
        line-height: 1.3em;
        text-align: left;
        margin: 0;
        color: #E1EDF4;

        @media (max-width: 768px) {
          font-size: 16px;
        }
      }

      .ep-name {
        font-family: 'PT Sans', sans-serif;
        font-size: 15px;
        line-height: 1.3em;
        text-align: left;
        color: #E1EDF4;
        text-transform: uppercase;
        margin-bottom: 15px;

        @media (max-width: 768px) {
          font-size: 13px;
        }
      }

      .rating {
        font-family: 'PT Sans', sans-serif;
        font-size: 15px;
        line-height: 1.3em;
        color: #E1EDF4;
        padding: 5px;
        border-radius: 5px;
        margin-left: 5px;

        @media (max-width: 768px) {
          font-size: 13px;
        }
      }
    }
  }

  > img {
    max-width: 100%;
  }


  p.comparison {
    font-size: 16px;
    max-width: 640px;
    margin: 15px auto;
    text-align: left;
    font-family: 'PT Sans', sans-serif;
    font-size: 15px;
    line-height: 1.3em;
    color: #E1EDF4;

    @media (max-width: 768px) {
      font-size: 13px;
    }
  }
}
</style>
