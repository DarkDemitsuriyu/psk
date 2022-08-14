<template>
  <div style="padding:50px; padding-top: 0px;">
    <psk-filters v-model="filters"></psk-filters>
    <div class="houses">
      <psk-house v-for="(house, i) in houses" :key="house" :id="house" :value="selectedHouse" :index="i" @click="clickHouse"></psk-house>
    </div>
    <hr/>
    <psk-flat-description v-if="getEntrances(selectedHouse).length > 0"></psk-flat-description>
    <div class="entrances">
      <div v-for="entrance in getEntrances(selectedHouse)" :key = "entrance.id" class="entrance">
        <div class="floor" v-for="floor in entrance.floors" :key="`${entrance.id}-${floor.floor}`">
          <div class="floor-numbers">
                {{floor.floor}}
          </div>
          <div class="flats">
            <psk-flat v-for="flat in floor.flats" :key="flat.id" :value="selectedFlats" :entrance="entrance.id" :number="flat.number" :filter="filters" :hovered="hoveredFlat" :obj="flats[flat.id]" @click="clickFlats" @hovered="hoverFlat"/>
          </div>
        </div>
        <br>
        <div v-text="entrance.title"></div>
      </div>
    </div>
    <psk-tooltip v-bind="tooltip"></psk-tooltip>
  </div>
</template>

<script>
import pskFlat from './components/flat.vue'
import pskHouse from './components/house.vue'
import pskTooltip from './components/tooltip.vue'
import pskFilters from './components/filters.vue'
import pskFlatDescription from './components/description_flat.vue'

export default {
  name: 'App',
  components: {
    pskFlat,
    pskHouse,
    pskTooltip,
    pskFilters,
    pskFlatDescription
  },
  data(){
    return {
      flats: {},
      houses: [],
      entrances: [],
      selectedHouse: null,
      selectedFlats: null,
      isFiltered: false,
      hoveredFlat:{
        floor: null,
        number: null,
        entrance: null
      },
      tooltip:{
        show: false,
        obj: null,
        event: null
      },
      filterHouses:[],
      filters:{
        costMin:null,
        costMax:null,
        squareMin: null,
        squareMax: null,
        subsidy:false,
        marginal: false,
        renovation: false,
        installment: false,
        status: "",
        plan_type: ""
      }
    }
  },
  async mounted(){
      let resp = await fetch("./data.json")
      let result = await resp.json()
      this.flats = result.flats
      this.houses = result.houses
      this.selectedHouse = result.houses[0]
      this.entrances = result.entrances
  },
  methods:{
    getEntrances(house){
      return this.entrances.filter( entrance => entrance.house_id == house)
    },
    clickHouse(house){
      this.selectedHouse = this.selectedHouse == house ? null : house
    },
    clickFlats(flats){
      this.selectedFlats = flats
    },
    hoverFlat(data){
      this.hoveredFlat = data
      this.tooltip.obj = data.data
      this.tooltip.show = data.data ? true : false
      this.tooltip.event = data.e
    }
  }
}
</script>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.houses{
  display:flex;
  justify-content:space-evenly;
}
.entrances {
    display: flex;
    flex-wrap: wrap;
    padding-top: 20px;
}
.entrance{
  display: flex;
  flex-direction:column;
  justify-content:flex-end;
  padding-bottom:20px;
}
.floor, .flats{
  display: flex;
}
.floor-numbers{
  padding: 5px;
  width: 18px;
  height: 18px;
}
</style>
