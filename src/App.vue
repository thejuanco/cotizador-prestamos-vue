<script setup>
  import Header from './components/Header.vue';

  //Sintaxis para options api
  // export default{
  //   components: {
  //     Header
  //   },
  // }

  function handleChange(e){
    console.log(e.target.value);
  }
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10 rounded-lg">
    <Header/>

    <div class="my-5">
      <input
        type="range"
        class="w-full bg-gray-200 accent-indigo-600 hover:accent-indigo-700"
        @input="handleChange"
      />
    </div>
  </div>
</template>

