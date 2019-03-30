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
    drilldown () {
      if (this.drilldown.season !== 0) {
        this.sceneData = this.data.filter(scene => {
          return scene.Image === this.drilldown.scene
        })[0]

        if (this.sceneData.Rating === 'TRUE') {
          this.$refs.rating.classList.add('green')
        } else if (this.sceneData.Rating === 'FALSE'){
          this.$refs.rating.classList.add('red')
        } else if (this.sceneData.Rating === 'MIXED'){
          this.$refs.rating.classList.add('purple')
        } else {
          this.$refs.rating.classList.add('grey')
        }
      }
    }
  }
}
</script>

<style lang="scss">
.description {

  img {
    max-width: 100%;
  }

  .title {
    p {
      display: inline-block;
    }
    p.rating {
      padding: 5px;
      margin-left: 10px;
      border-radius: 5px;
    }

    .green {
      background-color: green
    }
    .red {
      background-color: red
    }
    .purple {
      background-color: purple
    }
    .grey {
      background-color: grey
    }
  }

  p {
    font-size: 16px;

    @media (max-width: 768px) {
      font-size: 14px;
    }
  }
}
</style>
