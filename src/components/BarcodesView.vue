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
    <div class="m-2" v-for="item in props.bStorage">
        <img :src="item">
    </div>
</template>