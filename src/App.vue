<script setup>
  import { ref, reactive, computed, watch } from 'vue';
  import Header from './components/Header.vue';
  import Button from './components/Button.vue';
  import { calcularTotalPagar } from './helpers';

  const cantidad = ref(10000)
  // const state = reactive({
  //   cantidad: 0
  // })
  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;
  const meses = ref(6);
  const total = ref(0);

  //Sintaxis para options api
  // export default{
  //   components: {
  //     Header
  //   },
  // }
  const pagoMensual = computed(() => {
    return total.value / meses.value;
  })

  const formatearDinero = (valor) => {
    const formatter = new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
      maximumFractionDigits: 2
    })

    return formatter.format(valor) //Retorna la cantidad
  }

  const handleChangeDecremento = () => {
    const valor = cantidad.value - STEP;
    if(valor < MIN){
      alert('La cantidad no puede ser menor a 0')
      return
    }

    cantidad.value = valor
  }

  watch([cantidad, meses], () => {
    total.value = calcularTotalPagar(cantidad.value, meses.value)
  })

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
      <Button
        :operador="'-'"
        @fn="handleChangeDecremento"
      />
      <Button
        :operador="'+'"
        @fn="handleChangeIncremento"
      />
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

      <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">{{formatearDinero(cantidad)}}</p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->

      <h2 class="text-2xl font-extrabold text-gray-500 text-center">
        Elige un <span class="text-indigo-600">Plazo</span> a pagar
      </h2>

      <select class="w-full p-2 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500 mt-5"
        :value="meses"
        v-model.number="meses"
      >
        <option value="6">6 meses</option>
        <option value="12">12 meses</option>
        <option value="24">24 meses</option>
      </select>

      <div v-if="total > 0" class="my-5 space-y-3 bg-gray-100 rounded-lg p-5">
        <h2 class="text-2xl font-extrabold text-gray-500 text-center">
          Resumen <span class="text-indigo-600">de pagos</span>
        </h2>

        <p class="text-xl text-gray-500 text-center font-bold">{{meses}} Meses</p>
        <p class="text-xl text-gray-500 text-center font-bold">Total a pagar: {{formatearDinero(total)}}</p>
        <p class="text-xl text-gray-500 text-center font-bold">Mensuales: {{formatearDinero(pagoMensual)}}</p>
      </div>

      <p v-else class="text-center mt-2 text-gray-600">Selecciona una cantidad y un plazo</p>
    </div>
  </div>
</template>

