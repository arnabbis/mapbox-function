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
      zoom: 1.5,
      center: [-122.447303, 37.753574],
      // Choose from Mapbox's core styles, or make your own style with Mapbox Studio
      style: "mapbox://styles/mapbox/light-v10",
      
    },
  });

  function onMapLoaded(map: mapboxgl.Map) {
    map.addSource('mapbox-terrain', {
type: 'vector',
// Use any Mapbox-hosted tileset using its tileset id.
// Learn more about where to find a tileset id:
// https://docs.mapbox.com/help/glossary/tileset-id/
url: 'mapbox://mapbox.mapbox-terrain-v2'
});
map.addLayer({
'id': 'terrain-data',
'type': 'line',
'source': 'mapbox-terrain',
'source-layer': 'contour',
'layout': {
'line-join': 'round',
'line-cap': 'round'
},
'paint': {
'line-color': '#ff69b4',
'line-width': 1
}
});
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