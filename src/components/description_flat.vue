<template>
  <div class="flat-description">    
    <div>
      <div class="non_residential"></div>
      <span>Не жилое</span>
    </div>
    <div>
      <div class="apartment"></div>
      <span>Квартира</span>
    </div>  
    <div>
      <div class="parking"></div>
      <span>Паркинг</span>
    </div>
    <div>
      <div class="keys_issued"><i class="mdi mdi-lock-outline"></i></div>
      <span>Выданы ключи</span>
    </div>
    <div>
      <div class="reservation">Б</div>
      <span>Бронь</span>
    </div>
  </div>
  <div class="flat-description">
    <div>
      <div><i class="installment"></i></div>
      <span>С рассрочкой</span>
    </div>
    <div>
      <div><i class="renovation"></i></div>
      <span>С ремонтом</span>
    </div>
    <div>
      <div><i class="subsidy"></i></div>
      <span>Субсидированная</span>
    </div>
    <div>
      <div><i class="marginal"></i></div>
      <span>Маржинальная</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'psk-flat-description',
  props: {
    index: Number,
    id: {type: String, default: null},
    value: {type: String, default: 'null'},
  },
  emits: ['click'],
  computed:{
    isSelected(){
      return this.id == this.value
    }
  }
}
</script>

<style scoped>
.flat-description{
  display:flex;
  padding-top: 10px;
}
</style>