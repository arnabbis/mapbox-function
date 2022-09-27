<template>
    <div>
      <main class="w-screen h-screen">
        <head>
          <link
            href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css"
            rel="stylesheet"
          />
        </head>
        <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded" />
        <div id="menu" class="">
          <input
            id="satellite-v9"
            type="radio"
            name="rtoggle"
            value="satellite"
            checked="checked"
          />
          <label for="satellite-v9">satellite</label>
          <input id="light-v10" type="radio" name="rtoggle" value="light" />
          <label for="light-v10">light</label>
          <input id="dark-v10" type="radio" name="rtoggle" value="dark" />
          <label for="dark-v10">dark</label>
          <input id="streets-v11" type="radio" name="rtoggle" value="streets" />
          <label for="streets-v11">streets</label>
          <input id="outdoors-v11" type="radio" name="rtoggle" value="outdoors" />
          <label for="outdoors-v11">outdoors</label>
        </div>
      </main>
    </div>
  </template>
  <script setup lang="ts">
  
  import vMap from "v-mapbox";
  import mapboxgl from "mapbox-gl";
  
  //import globe from "globe"
  mapboxgl.accessToken =
    "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
  //const data: string;
  const state = reactive({
    map: {
      container: "map",
      zoom: 13.1,
      center: [-114.34411, 32.6141],
      pitch: 85,
      bearing: 80,
      // Choose from Mapbox's core styles, or make your own style with Mapbox Studio
      style: "mapbox://styles/mapbox-map-design/ckhqrf2tz0dt119ny6azh975y",
    },
  });
  function onMapLoaded(map: mapboxgl.Map) {
      map.addSource('mapbox-dem', {
  'type': 'raster-dem',
  'url': 'mapbox://mapbox.mapbox-terrain-dem-v1',
  'tileSize': 512,
  'maxzoom': 14
  });
  // add the DEM source as a terrain layer with exaggerated height
  map.setTerrain({ 'source': 'mapbox-dem', 'exaggeration': 1.5 });
  // add sky styling with `setFog` that will show when the map is highly pitched
  map.setFog({
  'horizon-blend': 0.3,
  'color': '#F8F0E3',
  'high-color': '#ADD8E6',
  'space-color': '#D8F2FF',
  'star-intensity': 0.0
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
  /* .marker {
        background-image: url("http://localhost:3000/assets/images/download.jpg");
        background-size: cover;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        cursor: pointer;
      }   */
  .mapboxgl-popup {
    max-width: 200px;
  }
  .mapboxgl-popup-content {
    text-align: center;
    font-family: "Open Sans", sans-serif;
  }
  #menu {
    position: absolute;
    background: #EFEFEF;
    padding: 10px;
    font-family: "Open Sans", sans-serif;
  }
  </style>