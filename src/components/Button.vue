<script setup>
//Recuperar los props
const props = defineProps({
    operador: String,
    fn: Function
})
</script>
<template>
    <button 
        type="button"
        class="h-10 w-10 flex items-center justify-center font-bold bg-indigo-500 rounded-full hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-indigo-500 text-white text-2xl"
        @click="fn"
    >{{operador}}</button>
</template>