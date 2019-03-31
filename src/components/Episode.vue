<template>
  <div class="episode">
    <div class="scene"
      v-for="(scene, index) in cleanData"
      :key="index"
      :ref="index + 1"
      :style="setStyle(scene)"
      @click="chosenScene(index + 1)">
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'season', 'episode', 'drilldown'],
  data () {
    return {
      colorMap: {
        'TRUE': 'green',
        'FALSE': 'red',
        'MIXED': 'purple',
        '': 'grey'
      },
      cleanData: [],
      totalDuration: 0,
      previousScene: 0,
      currentScene: 0
    }
  },
  mounted () {
    this.dataCleaning()
  },
  watch: {
    drilldown: {
      handler: function () {
        if (this.drilldown.season === this.season &&
          this.drilldown.episode === this.episode) {
          this.showScene(this.drilldown.scene)
        }
      },
      deep: true
    }
  },
  methods: {
    dataCleaning () {
      // remove HBO title and opening sequence
      this.cleanData = this.data.filter(scene => {
        return scene.Image !== null
      })
      // calculate duration
      this.cleanData.forEach(scene => {
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
    showScene (index) {
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
  .scene {
    width: 100%;

    &.current {
      width: 120%;
      margin-left: -10%;
    }
  }
}
</style>
