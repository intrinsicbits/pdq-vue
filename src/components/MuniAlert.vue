<template>
  <div class="muni grouping">
    <div>
      <label>2</label>
      <span>{{two.predictions[0]}}</span>
    </div>
    <div>
      <label>3</label>
      <span>{{three.predictions[0]}}</span>
    </div>
  </div>
</template>

<script>
import request from 'request'

export default {
  name: 'MuniAlert',
  data () { 
    return {
      muni: []
    }
  },
  computed: {
    two () {
      // console.log(this.muni)
      return this.muni[1]
    },
    three () {
      return this.muni[0]
    }
  },
  methods: {
    getMuniSchedule() {
      var vm = this;
      const MUNI_URI='http://localhost:3000/v1/muni'
      request.get(MUNI_URI, function(err, response, body) {
        const json = JSON.parse(body)
        vm.muni = json
      })
    },
    tick() {
      // every 2 mins
      setInterval(() => {
        this.getMuniSchedule()
      }, 1000 * 120)
    }
  },
  created() {
    this.getMuniSchedule()
    this.tick()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.theme-sanfrancisco .muni.grouping {
  position: absolute;
  top: .5em;
  left: 0;
}

.theme-sanfrancisco .muni.grouping div {
  overflow: hidden;
  font-size: 110px;
  text-align: right;
  min-height: 100px;
  min-width: 120px;
  background-color: rgba(0,0,0, 0.75);
  padding: 0.125em;
  margin-bottom: 0.125em;
  border-radius: 24px;
  font-weight: 300;
}

.theme-sanfrancisco .muni.grouping div > span {
  float: right;
}

.theme-sanfrancisco .muni.grouping label {
  font-size: 80px;
  font-weight: 300;
  float: left;
  min-width: 70px;
  display: inline-block;
  color: #F2E00C;
  font-size: 48px;
  text-align: left;
}
</style>