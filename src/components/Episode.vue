<template>
  <div class="episode">
    <div class="scene"
      v-for="(scene, index) in data"
      :key="index"
      :ref="index + 1"
      :style="setStyle(scene)"
      @click="chosenScene(index + 1)">
    </div>
    <p v-if="season === 1 || season === drilldown.season">EP {{ episode }}</p>
  </div>
</template>

<script>
export default {
  props: ['data', 'season', 'episode', 'drilldown'],
  data () {
    return {
      colorMap: {
        'TRUE': '#404E86',
        'FALSE': '#B23E4D',
        'MIXED': '#7994C3',
        '': '#C0CAC9'
      },
      totalDuration: 0,
      previousScene: 0,
      currentScene: 0
    }
  },
  mounted () {
    this.calculateDuration()
  },
  watch: {
    drilldown: {
      handler: function () {
        if (this.drilldown.episode === this.episode) {
          if (this.drilldown.season === this.season) {
            this.expandBar(this.drilldown.scene)
          } else if (this.drilldown.season === 0) {
            this.$refs[this.currentScene][0].classList.remove('current')
          }
        }

        if (this.drilldown.episode !== this.episode
          && this.currentScene !== 0) {
          this.$refs[this.currentScene][0].classList.remove('current')
        }
      },
      deep: true // to detect value change inside object
    }
  },
  methods: {
    calculateDuration () {
      this.data.forEach(scene => {
        this.totalDuration += this.toSeconds(scene.Duration)
      })
    },
    toSeconds (hms) {
      const arr = hms.split(':')
      const seconds = (+arr[0]) * 60 * 60 + (+arr[1]) * 60 + (+arr[2])
      return seconds
    },
    setStyle (scene) {
      const duration = this.toSeconds(scene.Duration)
      const percentage = +(duration / this.totalDuration * 100).toFixed(2)

      const color = this.colorMap[scene.Rating]

      return {
        height: percentage + '%',
        backgroundColor: color
      }
    },
    chosenScene (index) {
      this.$emit('chosen', {
        season: this.season,
        episode: this.episode,
        scene: index
      })
    },
    expandBar (index) {
      this.$refs[index][0].classList.add('current')
      this.previousScene = this.currentScene
      this.currentScene = index

      if (this.previousScene !== 0 && this.previousScene !== this.currentScene) {
        this.$refs[this.previousScene][0].classList.remove('current')
      }
    }
  }
}
</script>

<style lang="scss">
.episode {
  height: 200px;
  padding: 0 35%;
  margin: 0 auto;
  cursor: pointer;
  border-bottom: 1px solid rgba(121,148,195, 0.5);
  position: relative;

  @media (max-width: 768px) {
    padding: 0 30%;
  }

  @media (max-width: 480px) {
    padding: 0 25%;
  }

  .scene {
    width: 100%;

    &.current {
      width: 120%;
      margin-left: -10%;
    }
  }

  > p {
    position: absolute;
    left: 0;
    bottom: 0;
    margin: 5px 0;
    font-family: 'PT Sans', sans-serif;
    font-size: 15px;
    line-height: 1.3em;
    color: #E1EDF4;
  }
}
</style>
