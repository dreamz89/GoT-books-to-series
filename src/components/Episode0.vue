<template>
  <div>
    <div class="scene"
      v-for="(scene, index) in data"
      :key="index"
      :style="setStyle(scene)"
      @click="openModal(scene)">
    </div>
    <div class="modal"
      v-if="showModal"
      @click="showModal = false">
      <div class="content"
        @click.prevent.stop>
        <div class="close"
        @click="showModal = false">
          X
        </div>
        <img :src="getImage" />
        <p>TV</p>
        <p>{{ scene['TV'] }}</p>
        <p>Book</p>
        <p>{{ scene['Books'] }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'season', 'episode'],
  data () {
    return {
      showModal: false,
      scene: {},
      colorMap: {
        'TRUE': 'green',
        'FALSE': 'red',
        'MIXED': 'purple',
        '': 'grey'
      },
      total: this.toSeconds(this.data[this.data.length - 1]['Scene End'])
    }
  },
  computed: {
    getImage () {
      if (this.scene.Image) {
        return require('../images/season ' + this.season + '/GoT ' + this.season + ' ' + this.episode + ' ' + this.scene.Image + '.jpg')
      } else {
        return null
      }
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
      const percentage = +(duration / this.total * 100).toFixed(2)

      const color = this.colorMap[scene.Rating]

      return {
        height: percentage + '%',
        width: '100%',
        backgroundColor: color
      }
    },
    openModal (scene) {
      this.scene = scene
      this.showModal = true
    }
  }
}
</script>

<style lang="scss">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  height: 100%;
  width: 100%;
  background-color: rgba(0,0,0,0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;

  .content {
    position: relative;
    background-color: white;
    height: 100%;
    width: 100%;
    max-height: 500px;
    max-width: 500px;
    cursor: auto;
    overflow: scroll;

    .close {
      position: absolute;
      top: 0;
      right: 0;
      font-size: 28px;
      padding: 10px;
      cursor: pointer;
    }
  }
}
</style>
