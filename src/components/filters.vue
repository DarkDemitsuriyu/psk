<template>
  <div class="filters">
      <fieldset class="coast">
        <legend align="left">Цена</legend>
        <label>
          От <input type="number" min="0" v-model="data.costMin" />
        </label>
        <label> 
          До <input type="number" min="0" v-model="data.costMax" />
        </label>
      </fieldset>
      <fieldset class="square">
        <legend align="left">Площадь</legend>
        <label>
          От <input type="number" min="0" v-model="data.squareMin" />
        </label>
        <label> 
          До <input type="number" min="0" v-model="data.squareMax" />
        </label>
      </fieldset>
      <fieldset>
        <legend align="left">Другие</legend>
        <label>
          Статус
          <select v-model="data.status">
            <option value="">Все</option>
            <option>Выданы ключи</option>
            <option>Бронь</option>
            <option value="Договор">Свободна</option>
          </select>
        </label>
        <label>
          Тип планировки
          <select v-model="data.plan_type">
            <option value="">Все</option>
            <option>1K</option>
            <option>2K</option>
            <option>3K</option>
            <option>4K</option>
            <option>1E</option>
            <option>2E</option>
            <option>3E</option>
            <option>4E</option>
            <option>C</option>
          </select>
        </label>
        <br />
        <label>
          <input type="checkbox" v-model="data.subsidy" /> Наличие субсидии
        </label>
        <label> 
          <input type="checkbox" v-model="data.marginal" /> Наличие маржинальности
        </label>
        <label> 
          <input type="checkbox" v-model="data.renovation" /> Наличие ремонта
        </label>
        <label> 
          <input type="checkbox" v-model="data.installment" /> Наличие рассрочки
        </label>
      </fieldset>
    </div>
</template>

<script>
export default {
  name: 'psk-filters',
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed:{
    data:{
      get(){
        return this.modelValue
      },
      set(val){
        this.$$emit('update:modelValue', val)
      }
    }
  }
}
</script>

<style scoped>
.filters{
  display: flex;
  flex-flow: wrap;
}
.filters fieldset{
  text-align: left;
  flex-grow: 0;
  align-content: center;
  justify-content: center;
}
.coast input{
  width:84px;
}
.square input{
  width:40px;
}
</style>