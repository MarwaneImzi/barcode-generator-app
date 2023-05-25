<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue';
import BarcodesView from './components/BarcodesView.vue'
import BarcodeConvertor from './components/JsBarcodeTool.vue'

var barcodeProp = ref()
var barcode = ref()
var barecodeStorage = ref([])
var viewToggle = ref(false)
var listViewCSS = ref('')

console.log(viewToggle.value)

const SaveBarcode = () => {
  if (barcode.value != '' || barcode.value.trim() != '') {
    barcodeProp.value = barcode.value.toUpperCase().trim()
  }
}

const DeleteBarcodes = () => {
  localStorage.removeItem('barcodeData')
  barcode.value = ''
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
        
        <!-- Toggle list function  -->
        <div class="container mx-auto flex justify-center mb-2 noPrint">
          <span class="mx-3 text-sm font-medium text-gray-300">Printing</span>
          <label class="relative inline-flex items-center mx-5 cursor-pointer">
            <input type="checkbox" v-model="viewToggle" class="sr-only peer" checked>
            <div
              class="w-11 h-6 bg-gray-200 rounded-full peer dark:bg-gray-700 peer-focus:ring-4 peer-focus:ring-green-300 dark:peer-focus:ring-green-800 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-green-600">
            </div>
          </label>
          <span class="mx-3 text-sm font-medium text-gray-300">Scanning</span>
        </div>
        <div class="noPrint border-b-2 border-gray-700 container mx-auto"></div>
        
        
        <!-- Preview Box -->
        <div class="container mx-auto">
          <div class="noPrint hidden" style>{{ listViewCSS = (!viewToggle) ? 'flex flex-wrap-reverse justify-center' : 'flex flex-col flex-col-reverse justify-center' }}</div>
          <div :class="listViewCSS">
            <BarcodeConvertor :bProp="barcodeProp" style="display:none" />
            <!-- Really not good practice but i could not figure this out -->
            {{ wait() }}
            <BarcodesView :bStorage="barecodeStorage" :pToggle="viewToggle" />
          </div>
        </div>
        
        
        <div class="noPrint border-b-2 border-gray-700 container mx-auto"></div>
        
        <!-- Buttons  -->
        <div class="container mx-auto">
          <div class="flex mt-4 noPrint justify-around">
            <a @click="DeleteBarcodes"
              class="bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded">Clear</a>
            <a onclick="window.print()"
              class="bg-transparent hover:bg-green-500 text-green-700 font-semibold hover:text-white py-2 px-4 border border-green-500 hover:border-transparent rounded">Print</a>
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
}
</style>
