<script setup>
import { onMounted, onUpdated, ref } from 'vue';

var props = defineProps(['bStorage'])
onMounted(() => {
})
onUpdated(() => {
    console.log(props.bStorage)
})

console.log(props.bStorage)


</script>

<template>

    <br>
    <div v-for="item in props.bStorage" class="">
        <img :src="item">
    </div>
</template>