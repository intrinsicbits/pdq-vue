<template>
  <div class="date grouping">
    
    <h3>{{today}}</h3>
    <h1>{{localTime}}</h1>
    <h3 id="kst">{{koreaTime}}</h3>
    
  </div>
</template>

<script>
import moment from 'moment-timezone'

export default {
  name: 'WorldTime',
  data () {
    return {
      now: moment()
    }
  },
  computed: {
    today () {
      return this.now.format('ddd, MMM Do')
    },
    localTime () {
      return this.now.format('h:mm')
    },
    koreaTime () {
      // need to clone this or it will mutate now to this TZ
      return moment(this.now).tz('Etc/GMT-9').format('HHmm ddd')
    }
  },
  methods: {
    tick() {
      // every second
      setInterval(() => {
        this.now = moment()
      }, 1000)
    }
  },
  created() {
    this.tick()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

.date.grouping {
  margin-right 0em
  position absolute
  bottom 1em
  right .5em
}

.date.grouping h1 {
  text-align right
  font-size 230px
  line-height 230px
  margin 0
  padding 0
  letter-spacing -8px
}

.date.grouping h3 {
  text-align right
  font-size 100px
  line-height 100px
  margin 0
  padding 0
  letter-spacing -6px
}
</style>
