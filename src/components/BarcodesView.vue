<script setup>
import { onMounted, onUpdated, ref } from 'vue';

var barecodeStorage = ref([])
barecodeStorage.value = JSON.parse(localStorage.getItem('barcodeData'))

console.log('Barcode View Test')
console.log(barecodeStorage)

</script>

<template>
    <div>{{ barecodeStorage }}</div>
</template>