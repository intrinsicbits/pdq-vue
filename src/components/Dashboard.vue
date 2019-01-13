<template>
  <div class="theme-sanfrancisco">
    <MuniAlert />
    <Weather />
    <WorldTime />
  </div>
</template>

<script>
import MuniAlert from '../components/MuniAlert.vue'
import Weather from '../components/Weather.vue'
import WorldTime from '../components/WorldTime.vue'

export default {
  name: 'Dashboard',
  props: {
    msg: String
  },
  components: {
    MuniAlert,
    Weather,
    WorldTime
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus">
.theme-sanfrancisco 
  color #f1f1f1
  font-weight 100

.theme-sanfrancisco h1,
.theme-sanfrancisco h2,
.theme-sanfrancisco h3,
.theme-sanfrancisco h4,
.theme-sanfrancisco h5,
.theme-sanfrancisco h6 {
  font-family: 'roboto';
  font-weight: 100;
  color: #f1f1f1;
}

.grouping
  float right
  margin-right .5em
  margin-left .5em
  font-size 60px

.right-label-small {
  font-size: 48px;
  line-height: 48px;
  color: #A1A1A1;
  margin: 0;
  padding: 0;
  text-transform: uppercase;
}

.currency-symbol {
  font-size: 32px;
  line-height: 72px;
}

</style>
