<template>
  <div>
        <main class="w-screen h-screen">

            <head>
                <link href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css" rel="stylesheet" />
            </head>
            <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded" />
            <div id="menu">
<input id="satellite-v9" type="radio" name="rtoggle" value="satellite" checked="checked">
<!-- See a list of Mapbox-hosted public styles at -->
<!-- https://docs.mapbox.com/api/maps/styles/#mapbox-styles -->
<label for="satellite-v9">satellite</label>
<input id="light-v10" type="radio" name="rtoggle" value="light">
<label for="light-v10">light</label>
<input id="dark-v10" type="radio" name="rtoggle" value="dark">
<label for="dark-v10">dark</label>
<input id="streets-v11" type="radio" name="rtoggle" value="streets">
<label for="streets-v11">streets</label>
<input id="outdoors-v11" type="radio" name="rtoggle" value="outdoors">
<label for="outdoors-v11">outdoors</label>
</div>
        </main>
    </div>
</template>

<script setup lang="ts">
    import vMap from "v-mapbox";
import mapboxgl from "mapbox-gl";

mapboxgl.accessToken =
    "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
//const data: string;
const state = reactive({
    map: {
        container: "map",
        zoom: 10,
        center: [30.0222, -1.9596],
        // Choose from Mapbox's core styles, or make your own style with Mapbox Studio
        style: "mapbox://styles/mapbox/streets-v11",

    },
});

function onMapLoaded(map: mapboxgl.Map) {
const layerList = document.getElementById('menu');
const inputs = layerList.getElementsByTagName('input');
 
for (const input of inputs) {
input.onclick = (layer) => {
const layerId = layer.target.id;
map.setStyle('mapbox://styles/mapbox/' + layerId);
};
}
}
</script>

<style>

</style>