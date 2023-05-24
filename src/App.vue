<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue';
import BarcodesView from './components/BarcodesView.vue'
import BarcodeConvertor from './components/JsBarcodeTool.vue'

var barcodeProp = ref()
var barcode = ref()
var barecodeStorage = ref([])


const SaveBarcode = () => {
  barcodeProp.value = barcode.value.toUpperCase().trim()
  console.log(barcode)
}

const DeleteBarcodes = () => {
  localStorage.removeItem('barcodeData')
  barcodeProp.value = ''
  barcodeProp.value = 'cleared'
}

function wait() {
  setTimeout(function () {
    barecodeStorage.value = JSON.parse(localStorage.getItem('barcodeData'))
  }, 1000)
}
</script>

<template>
  <div>
    <div>
      <!-- input area -->
      <div class="text-gray-400 bg-slate-900 body-font relative h-full min-h-screen">
        <div class="container px-5 pt-24 mx-auto noPrint">
          <div class="flex flex-col text-center w-full mb-12">
            <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-white">Barcode Generator</h1>
            <p class="lg:w-2/3 mx-auto leading-relaxed text-base">Generate barcodes for printing and scanning</p>
          </div>
          <div class="lg:w-1/2 md:w-2/3 mx-auto">
            <div class="flex flex-wrap -m-2">

              <div class="p-2 w-full">
                <div class="relative">
                  <label for="barcode" class="leading-7 text-sm text-gray-400">Barcode (Code128)</label>
                  <input type="text" v-model.trim="barcode" v-on:keyup.enter="SaveBarcode"
                    style="text-transform: uppercase;"
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
        <div class="flex my-4 justify-center">
          <button @click="DeleteBarcodes"
            class="noPrint flex mx-2 text-black bg-slate-300 border-0 py-2 px-2 focus:outline-none hover:bg-red-600 rounded text-lg"><img
              src="./assets/trash-2.svg" alt="Clear Storage"></button>
          <button onclick="window.print()"
            class="noPrint flex mx-2 text-white bg-slate-300 border-0 py-2 px-2 focus:outline-none hover:bg-green-600 rounded text-lg"><img
              src="./assets/printer.svg" alt="Print"></button>
        </div>

        <!-- Preview Box -->
        <div class="container mx-auto">
          <div class="flex flex-wrap-reverse justify-center">
            <BarcodeConvertor :bProp="barcodeProp" style="display:none" />
            <!-- Really not good practice but i could not figure this out -->
            {{ wait() }}
            <BarcodesView :bStorage="barecodeStorage" />

          </div>
        </div>



      </div>
    </div>
  </div>
  <footer class="text-gray-400 bg-slate-900 body-font noPrint">
    <div class="container px-5 py-8 mx-auto flex items-center sm:flex-row flex-col">
      <p class="text-sm text-gray-400 sm:ml-4 sm:pl-4 sm:border-l-2 sm:border-gray-800 sm:py-2 sm:mt-0 mt-4">© 2023
        Marwane —
        <a href="https://github.com/MarwaneImzi" class="text-gray-500 ml-1" target="_blank"
          rel="noopener noreferrer">MarwaneImzi</a>
      </p>
    </div>
  </footer>
</template>

<style scoped>
@media print {
  .noPrint {
    display: none;
  }

}

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
}</style>
