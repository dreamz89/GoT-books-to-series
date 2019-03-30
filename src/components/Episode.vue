<template>
  <div class="episode">
    <div class="scene"
      v-for="(scene, index) in cleanData"
      :key="index"
      :style="setStyle(scene)"
      @click="expandSeason(index + 1)">
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'season', 'episode'],
  data () {
    return {
      colorMap: {
        'TRUE': 'green',
        'FALSE': 'red',
        'MIXED': 'purple',
        '': 'grey'
      },
      cleanData: [],
      totalDuration: 0
    }
  },
  mounted () {
    this.dataCleaning()
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
        width: '100%',
        backgroundColor: color
      }
    },
    expandSeason (scene) {
      this.$emit('expand', {
        season: this.season,
        episode: this.episode,
        scene: scene
      })
    }
  }
}
</script>

<style lang="scss">
</style>
