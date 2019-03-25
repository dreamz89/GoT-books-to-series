<template>
  <div>
    <div class="scene"
      v-for="(scene, index) in data"
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
      totalDuration: this.toSeconds(this.data[this.data.length - 1]['Scene End'])
    }
  },
  methods: {
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
