<script setup>
import JsBarcode from 'jsbarcode'
import { onUpdated, ref } from 'vue';

var props = defineProps(['bProp'])
var url = ref('')   

onUpdated(() => {
    JsBarcode('#barcodeid', props.bProp)
    SaveBarcodeSVG()
})

function SaveBarcodeSVG() {
    //https://stackoverflow.com/questions/23218174/how-do-i-save-export-an-svg-file-after-creating-an-svg-with-d3-js-ie-safari-an
    //get svg element.
    var svg = document.getElementById("barcodeid");


    //get svg source.
    var serializer = new XMLSerializer();
    var source = serializer.serializeToString(svg);

    //add name spaces.
    if (!source.match(/^<svg[^>]+xmlns="http\:\/\/www\.w3\.org\/2000\/svg"/)) {
        source = source.replace(/^<svg/, '<svg xmlns="http://www.w3.org/2000/svg"');
    }
    if (!source.match(/^<svg[^>]+"http\:\/\/www\.w3\.org\/1999\/xlink"/)) {
        source = source.replace(/^<svg/, '<svg xmlns:xlink="http://www.w3.org/1999/xlink"');
    }

    //add xml declaration
    source = '<?xml version="1.0" standalone="no"?>\r\n' + source;

    //convert svg source to URI data scheme.
    url = "data:image/svg+xml;charset=utf-8," + encodeURIComponent(source);

    SaveURL(url)

}

function SaveURL(url) {
    var new_data = url
    // if there is nothing saved at the start then save an empty arry
    if (localStorage.getItem('barcodeData') == null) {
        localStorage.setItem('barcodeData', '[]')
    }

    // get old data to add new data
    var old_data = JSON.parse(localStorage.getItem('barcodeData'))
    
    old_data.push(new_data)

    // save the old + new data to local storage
    localStorage.setItem('barcodeData', JSON.stringify(old_data))
}

</script>

<template>
    <svg id="barcodeid" class=" w-11/12"></svg>
</template>