<template>
  <div>
        <main class="w-screen h-screen">

            <head>
                <link href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css" rel="stylesheet" />
            </head>
            <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded" />
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
        center: [78.9629,20.5937],
        // Choose from Mapbox's core styles, or make your own style with Mapbox Studio
        style: "mapbox://styles/mapbox/light-v10",

    },
});

function onMapLoaded(map: mapboxgl.Map) {
    map.addSource('rwanda-provinces', {
'type': 'geojson',
'data': 'https://docs.mapbox.com/mapbox-gl-js/assets/rwanda-provinces.geojson'
});
map.addLayer({
'id': 'rwanda-provinces',
'type': 'fill',
'source': 'rwanda-provinces',
'layout': {},
'paint': {
'fill-color': [
'let',
'density',
['/', ['get', 'population'], ['get', 'sq-km']],
[
'interpolate',
['linear'],
['zoom'],
8,
[
'interpolate',
['linear'],
['var', 'density'],
274,
['to-color', '#edf8e9'],
1551,
['to-color', '#006d2c']
],
10,
[
'interpolate',
['linear'],
['var', 'density'],
274,
['to-color', '#eff3ff'],
1551,
['to-color', '#08519c']
]
]
],
'fill-opacity': 0.7
}
});
}

</script>

<style>

</style>