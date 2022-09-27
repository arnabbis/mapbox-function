import mapboxgl from "mapbox-gl";

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
import mapboxgl from "mapbox-gl";
import vMap from "v-mapbox";

mapboxgl.accessToken = "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
const state = reactive({
    map: {
        container: "map",
        zoom: 1.5,
        center: [-75.789, 41.874],
        // Choose from Mapbox's core styles, or make your own style with Mapbox Studio
        style: "mapbox://styles/mapbox/dark-v10",

    },
});

function onMapLoaded(map: mapboxgl.Map) {
    // map.on('load', () => {
    map.addSource('radar', {
        'type': 'image',
        'url': 'C:\Users\arnab.biswas1\Desktop\mapbox functions\map-box\assets\radar.gif',
        'coordinates': [
            [-80.425, 46.437],
            [-71.516, 46.437],
            [-71.516, 37.936],
            [-80.425, 37.936]
        ]
    });
    map.addLayer({
        id: 'radar-layer',
        'type': 'raster',
        'source': 'radar',
        'paint': {
            'raster-fade-duration': 0
        }
    });
    // });
}
</script>

<style>
.w-screen {
    width: 100vw;
}

.h-screen {
    height: 100vh;
}

.h-full {
    height: 100%;
}

.w-full {
    width: 100%;
}
</style>