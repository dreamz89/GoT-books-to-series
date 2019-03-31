<template>
  <div class="description">
    <img :src="'images/season ' + drilldown.season + '/GoT ' + drilldown.season + ' ' + drilldown.episode + ' '  + drilldown.scene + '.jpg'"/>
    <div class="title">
      <p>{{ sceneData.Scene }}</p>
      <p class="rating" ref="rating">{{ sceneData.Rating }}</p>
    </div>
    <p>{{ sceneData.Difference }}</p>
  </div>
</template>

<script>
export default {
  props: ['data', 'drilldown'],
  data () {
    return {
      sceneData: {}
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
          this.$refs.rating.style.backgroundColor = 'green'
        } else if (this.sceneData.Rating === 'FALSE'){
          this.$refs.rating.style.backgroundColor = 'red'
        } else if (this.sceneData.Rating === 'MIXED'){
          this.$refs.rating.style.backgroundColor = 'purple'
        } else {
          this.$refs.rating.style.backgroundColor = 'grey'
        }
      }
    }
  }
}
</script>

<style lang="scss">
.description {
  width: 100%;

  img {
    max-width: 100%;
  }

  .title {
    margin: 15px 0;

    p {
      display: inline-block;
    }
    p.rating {
      padding: 5px;
      margin-left: 10px;
      border-radius: 5px;
    }
  }

  p {
    font-size: 16px;
    max-width: 600px;
    margin: 0 auto;

    @media (max-width: 768px) {
      font-size: 14px;
    }
  }
}
</style>
