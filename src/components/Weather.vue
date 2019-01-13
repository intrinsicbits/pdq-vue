<template>
  <div class="weather grouping">

    <div class="current-temp">
      <div class="daypod feature">
        <skycon :condition="todayWeather.icon" width="144" height="144" color="#EFEFEF"></skycon>
      </div>
      {{ parseInt(todayWeather.temperature, 10) }}&deg;
      {{ parseInt((todayWeather.temperature - 32) / 1.8000, 10) }}&deg;
      <br>
      <span class="text-forecast">
        Rain tomorrow through Thursday, with high temperatures rising to 59°F next Sunday
      </span>
    </div>

    <div class="daypod" v-for="(day) in dailyWeather" :key="day.date">
      <div class="skycon">
        <skycon :condition="day.icon" width="72" height="72" color="#AFAFAF"></skycon>
      </div>
      <div class="weather-temps">
        <span class="low">{{parseInt(day.temperatureMin)}}</span>
        <span class="high">{{parseInt(day.temperatureMax)}}</span>
      </div>
      <div class="weather-date">
        {{convertEpoch(day.time)}}
      </div>
    </div>
    
  </div>
</template>

<script>
import moment from 'moment'
import request from 'request'

export default {
  name: 'Weather',
  data () { 
    return {
      forecast: {
        currently: {
          icon: 'clear'
        }
      }
    }
  },
  computed: {
    todayWeather () {
      console.log('todayWeather')
      console.log(this.forecast.currently)
      return this.forecast.currently || []
    },
    dailyWeather () {
      console.log('dailyWeather')
      console.log(this.forecast.daily)
      return this.forecast.daily ? this.forecast.daily.data : []
    }
  },
  methods: {
    convertEpoch(time) {
      return moment.unix(time).format('ddd')
    },
    getForecast() {
      var vm = this;
      const FORECAST_URI='http://localhost:3000/v1/weather'
      request.get(FORECAST_URI, function(err, response, body) {
        var json = JSON.parse(body)
        vm.forecast = json
        console.log(vm.forecast)
      })
    },
    tick() {
      // every 6 hours
      setInterval(() => {
        this.getForecast()
      }, 1000 * 60 * 60)
    }
  },
  created() {
    this.getForecast()
    this.tick()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

.weather.grouping {
  position absolute
  left 0em
  bottom 2em
}

.daypod {
  float left
  background-color rgba(0,0,0, 0.55)
  margin-right 0.125em
  border-radius 28px
}

.daypod canvas {
  width 92px
  margin 24px 24px 0 24px
}

.weather.grouping div label {
  float left
  font-size 28px
}

.current-temp {
  font-size 128px
  line-height 130px
  margin-right 0.125em
  font-weight 300
}

.text-forecast {
  padding 0
  margin 0
  font-size 32px
  float left
  line-height 1.5
}

.weather-temps {
  font-size 36px
  text-align center
}
.weather-temps .high {
  color #FBD1FA
}
.weather-temps .low {
  margin-right 10px
  color #AFE9FB
}

.weather-date {
  margin .2em
  padding-top .2em
  border-top 1px solid #333
  font-size 24px
  text-transform uppercase
  text-align center
}
</style>
