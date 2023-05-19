<script setup>
import { onMounted, onUpdated, ref } from 'vue';

var props = defineProps(['bStorage'])
onMounted(() => {
    props.bStorage = JSON.parse(localStorage.getItem('barcodeData'))
})
onUpdated(() => {
    console.log(props.bStorage)
    
})
console.log(props.bStorage)


</script>

<template>
    <div v-for="item in props.bStorage" class="">
        <img :src="item">
    </div>
</template>