<script setup>
import { onMounted, onUpdated, ref } from 'vue';

var props = defineProps(['bStorage'])

</script>

<template>

    <br>
    <div class="m-2" v-for="item in props.bStorage">
        <img :src="item">
    </div>
</template>