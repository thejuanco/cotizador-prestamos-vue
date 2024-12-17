<script setup>
  import { ref, reactive } from 'vue';
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

  function handleChange(e){
    //modificando el state
    // state.cantidad = Number(e.target.value);

    cantidad.value = Number(e.target.value);
  }
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10 rounded-lg">
    <Header/>

    <div class="my-5">
      <input
        class="w-full bg-gray-200 accent-indigo-600 hover:accent-indigo-700"
        type="range"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        :value="cantidad"
        @input="handleChange"
      />

      <p>{{cantidad}}</p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->
    </div>
  </div>
</template>

