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
          this.$refs.rating.style.backgroundColor = '#404E86'
        } else if (this.sceneData.Rating === 'FALSE'){
          this.$refs.rating.style.backgroundColor = '#B23E4D'
        } else if (this.sceneData.Rating === 'MIXED'){
          this.$refs.rating.style.backgroundColor = '#7994C3'
        } else {
          this.$refs.rating.style.backgroundColor = '#C0CAC9'
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
    text-align: left;
    font-family: 'PT Sans', sans-serif;
    font-size: 15px;
    line-height: 1.3em;
    color: #E1EDF4;

    @media (max-width: 768px) {
      font-size: 14px;
    }
  }
}
</style>
