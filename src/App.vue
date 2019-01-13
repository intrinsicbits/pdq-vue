<template>
  <div id="app">
    <Dashboard msg="pdq.io dashboard resurrection"/>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard.vue'

export default {
  name: 'app',
  components: {
    Dashboard
  }
}
</script>
<style lang="stylus">
@import url('https://fonts.googleapis.com/css?family=Roboto:100,300,500,700,900');

body
  font-family 'Roboto'
  font-weight 100
  margin 0
  padding 0
  background-color #242424
  width 1920px
  height 1080px
  overflow hidden
  background #242424 url(./assets/ggb1920.jpg) top left no-repeat
  color #F0F0F

#app
  position relative
  width 1920px
  height 1080px
  text-shadow 2px 2px 2px rgba(0, 0, 0, 1)
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  margin-top 60px

</style>
