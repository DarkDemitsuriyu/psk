<template>
  <dl v-show="show" ref="tooltip" class="tooltip" :style="style">
      {{ data.type }}<br/>
      <dt>Статус:</dt> <dd>{{ data.status == 'Договор' ? 'Свободна' : data.status }}</dd>
      <dt>Цена:</dt> <dd>{{ data.cost.toLocaleString() }} &#8381;</dd>
      <dt>Этаж:</dt> <dd>{{ data.floor }}</dd>
      <dt>Номер квартиры:</dt> <dd>{{ data.number }}</dd>
      <dt>Площадь:</dt> <dd>{{ data.square }} кв.м</dd>
      <dt>Тип планировки:</dt> <dd>{{ data.plan_type }}</dd>
      <dt>Субсидированная:</dt> <dd>{{ data.subsidy ? 'Да' : 'Нет' }}</dd>
      <dt>Маржинальная:</dt> <dd>{{ data.marginal ? 'Да' : 'Нет' }}</dd>
      <dt>С ремонтом:</dt> <dd>{{ data.renovation ? 'Да' : 'Нет' }}</dd>
      <dt>С рассрочкой:</dt> <dd>{{ data.installment ? 'Да' : 'Нет' }}</dd>
  </dl>
</template>

<script>
export default {
  name: 'psk-tooltip',
  props: {
    obj: {type: Object, default: () => {}},
    show: Boolean,
    event: Object
  },
  computed:{
    data(){
      return this.obj ? this.obj : {cost:0}
    },
    style(){
      let coord = {
        left: '0px',
        top: '0px'
      }
      if(this.event){
        let box = this.event.target.getBoundingClientRect()
        let left = box.left + window.pageXOffset
        let top = box.top + window.pageYOffset
        let x1 = (window.innerWidth + window.pageXOffset) - (left + 300)
        let x = x1 <=0 ? left - 264 : left + 28
        let y1 = (window.innerHeight + window.pageYOffset) - (top + 250)
        let y = y1 <=0 ? top - 200 -28 : top + 28
        coord.left = `${x}px`
        coord.top = `${y}px`
      }
      return coord
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tooltip{
  border-bottom: 1px dotted #0077AA;
  background: rgba(43, 42, 42, 0.8);
	border-radius: 8px 8px 8px 8px;
	box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.5);
	color: #FFF;
	padding: 5px 7px;
	position: absolute;
  z-index: 50;
	transition: all 0.4s ease-in-out; /* Добавить плавности по вкусу */
  width: 250px;
  height: 200px;
  text-align: left;
}
.tooltip dt{
  float: left;
  margin-right: 10px;
}
</style>
