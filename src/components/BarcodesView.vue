<script setup>
var props = defineProps(['bStorage', 'pToggle'])
</script>

<template>
    <br>
    <span v-if="!props.pToggle" class="m-2" v-for="item in props.bStorage">
        <img :src="item">
    </span>
    <span v-else class=" my-7 mx-auto" v-for="item in props.bStorage">
        <img :src="item" width="400">
    </span>
</template>