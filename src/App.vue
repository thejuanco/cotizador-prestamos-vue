<script setup>
  import { ref, reactive, computed } from 'vue';
  import Header from './components/Header.vue';

  const cantidad = ref(10000)
  // const state = reactive({
  //   cantidad: 0
  // })
  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  //Sintaxis para options api
  // export default{
  //   components: {
  //     Header
  //   },
  // }

  const formatearDinero = computed(() => {
    const formatter = new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
      maximumFractionDigits: 2
    })

    return formatter.format(cantidad.value) //Retorna la cantidad
  })

  const handleChangeDecremento = () => {
    const valor = cantidad.value - STEP;
    if(valor < MIN){
      alert('La cantidad no puede ser menor a 0')
      return
    }

    cantidad.value = valor
  }

  const handleChangeIncremento = () => {
    const valor = cantidad.value + STEP;
    if(valor > MAX){
      alert('La cantidad no puede ser mayor a 20,000')
      return
    }
    cantidad.value = valor
  }
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10 rounded-lg">
    <Header/>

    <div class="flex justify-between mt-10">
      <button class="h-10 w-10 flex items-center justify-center font-bold bg-indigo-500 rounded-full hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-indigo-500 text-white text-2xl"
        @click="handleChangeDecremento"
      >-</button>
      <button class="h-10 w-10 flex items-center justify-center font-bold bg-indigo-500 rounded-full hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-indigo-500 text-white text-2xl"
        @click="handleChangeIncremento"
      >+</button>
    </div>

    <div class="my-5">
      <input
        class="w-full bg-gray-200 accent-indigo-600 hover:accent-indigo-700"
        type="range"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        v-model.number="cantidad"
      />

      <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">{{formatearDinero}}</p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->
    </div>
  </div>
</template>

