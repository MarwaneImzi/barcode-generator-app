<script setup>
import { ref } from 'vue';
import BarcodesView from './components/BarcodesView.vue'
import BarcodeConvertor from './components/JsBarcodeTool.vue'

var barcodeProp = ref()
var barcode = ref()

const SaveBarcode = () => {
  barcodeProp.value = barcode.value
}

</script>

<template>
  <div>
    <div>
      <!-- input area -->
      <div class="text-gray-400 bg-slate-900 body-font relative h-full min-h-screen">
        <div class="container px-5 py-24 mx-auto">
          <div class="flex flex-col text-center w-full mb-12">
            <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-white">Barcode Generator</h1>
            <p class="lg:w-2/3 mx-auto leading-relaxed text-base">Generate barcodes for printing and scanning</p>
          </div>
          <div class="lg:w-1/2 md:w-2/3 mx-auto">
            <div class="flex flex-wrap -m-2">

              <div class="p-2 w-1/2">
                <div class="relative">
                  <label for="barcode" class="leading-7 text-sm text-gray-400">Barcode (Code128)</label>
                  <input type="text" v-model="barcode" v-on:keyup.enter="SaveBarcode"
                    class="w-full bg-gray-800 bg-opacity-40 rounded border border-gray-700 focus:border-green-500 focus:bg-gray-900 focus:ring-2 focus:ring-green-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                </div>
              </div>

              <div class="p-2 w-full">
                <button @click="SaveBarcode"
                  class="flex mx-auto text-white bg-green-500 border-0 py-2 px-8 focus:outline-none hover:bg-green-600 rounded text-lg">Generate</button>
              </div>
              <div class="p-2 w-full pt-8 mt-8border-t border-gray-800 text-center"></div>
            </div>
          </div>
        </div>

        <!-- Preview Box -->
        <BarcodeConvertor :bProp="barcodeProp" />
        <BarcodesView/>
      </div>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
