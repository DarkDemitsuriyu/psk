<template>
  <div class="flat" :class="classMain" @click="clickFlat" @mouseenter="mouseenter" @mouseleave="mouseleave">
    <i v-show="obj.installment" class="installment"></i>
    <i v-show="obj.renovation" class="renovation"></i>
    <i v-show="obj.marginal" class="marginal"></i>
    <i v-show="obj.subsidy" class="subsidy"></i>

    <i v-show="obj.status == 'Выданы ключи'" class="mdi mdi-lock-outline"></i>
    <span v-show="obj.status == 'Бронь'">Б</span>
    <span v-show="obj.status != 'Бронь' && obj.status != 'Выданы ключи'" v-text="obj.plan_type"></span>
  </div>
</template>

<script>
export default {
  name: 'psk-flat',
  props: {
    obj: {type: Object, default: ()=>{}},
    hovered: {type: Object, default: ()=>{}},
    filter: {type: Object, default: ()=>{}},
    number: Number,
    entrance: String,
    value: String
  },
  emits:['click', 'hovered'],
  computed:{
    isDisabled(){
      let isValid = true
      if(this.filter.costMin){
        isValid = isValid && this.filter.costMin <= this.obj.cost
      }
      if(this.filter.costMax){
        isValid = isValid && this.filter.costMax >= this.obj.cost
      }
      if(this.filter.squareMin){
        isValid = isValid && this.filter.squareMin <= this.obj.square
      }
      if(this.filter.squareMax){
        isValid = isValid && this.filter.squareMax >= this.obj.square
      }
      if(this.filter.renovation){
        isValid = isValid && this.filter.renovation && this.obj.renovation
      }
      if(this.filter.subsidy){
        isValid = isValid && this.filter.subsidy && this.obj.subsidy
      }
      if(this.filter.marginal){
        isValid = isValid && this.filter.marginal && this.obj.marginal
      }
      if(this.filter.installment){
        isValid = isValid && this.filter.installment && this.obj.installment
      }
      if(this.filter.status){
        isValid = isValid && this.filter.status == this.obj.status
      }
      if(this.filter.plan_type){
        isValid = isValid && this.filter.plan_type == this.obj.plan_type
      }
      return !isValid
    },
    isSelected(){
      return this.obj.id == this.value
    },
    isHovered(){
      return (this.hovered.floor == this.obj.floor || this.hovered.number == this.number) && this.entrance == this.hovered.entrance
    },
    classMain(){
      return [{
        'non_residential': this.obj.type == "Нежилые помещения",
        'apartment': this.obj.type == "Квартира",
        'parking': this.obj.type == "Паркинг",
        'keys_issued': this.obj.status == "Выданы ключи",
        'reservation': this.obj.status == "Бронь",
        'selected': this.isSelected,
        'hovered': this.isHovered,
        'disabled': this.isDisabled,
      }, `flat-floor-${this.obj.floor}`, `flat-number-${this.number}`]
    }
  },
  methods:{
    clickFlat(){
      this.$emit('click', this.obj.id)
    },
    mouseenter(e){
      if(!this.isDisabled){
        this.$emit('hovered', {floor: this.obj.floor, number: this.number, entrance: this.entrance, data: this.obj, e})
      }      
     },
    mouseleave(){
      if(!this.isDisabled){
        this.$emit('hovered', {floor: null, number: null, entrance: null, data: null, e: null})
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.flat:hover:not(.disabled){
  background: rgb(0, 153, 255) !important;
  border: 1px solid black !important;
}
.flat.selected:not(.disabled){
  background: rgb(0, 153, 255) !important;
  border: 1px solid black !important;
}
.flat > span{
  vertical-align: middle;
}
.hovered{
  opacity: 0.4;
}
.disabled{
  cursor: default;
  background:rgb(179, 179, 179) !important;
  color:rgb(179, 179, 179);
}
.mdi {
    vertical-align: middle;
    line-height: 18px;
}
</style>
