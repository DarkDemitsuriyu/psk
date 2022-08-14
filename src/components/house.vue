<template>
  <div :class="{'house': true, 'selected':isSelected}" @click="$emit('click', id)">
    <img alt="Фото дома" src="https://webstockreview.net/images/floor-clipart-isometric-9.png">
    <div>ГП-{{ index + 1 }}</div>
  </div>
</template>

<script>
export default {
  name: 'psk-house',
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.house{
  height: auto;
  cursor: pointer;
}
.house.selected{
  background:rgba(0, 140, 255, 0.185);
}
.house:hover{
  opacity: 0.5;
}
.house img{
  max-height: 70px;
}
</style>
