<template>
<div>
 <l-map
   :center="center"
   :zoom="zoom"
   class="map"
   ref="map"
   @update:zoom="zoomUpdated"
   @update:center="centerUpdated"
 >
   <l-tile-layer
     :url="url"
   >
   </l-tile-layer>
   </l-map>
      <button @click="locatorButtonPressed(); ">pokaż lokalizacje</button>

</div>
</template>

<script>
import { LMap, LTileLayer } from '@vue-leaflet/vue-leaflet';
import 'leaflet/dist/leaflet.css';

export default {
 components: {
   LMap,
   LTileLayer
 },
 data () {
   return {
     url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
     center: [ 52.24900435980021, 21.02134262909435 ],
     zoom: 15,
   }
 },
 methods: {
   zoomUpdated (zoom) {
     this.zoom = zoom;
     console.log(this.markers)
   },
   centerUpdated (center) {
     this.center = center;
   },
   locatorButtonPressed() {
   navigator.geolocation.getCurrentPosition(
      position => {
        this.center = [position.coords.latitude, position.coords.longitude]
        this.centerUpdated(this.center);

      },
      error => {
         console.log(error.message);
      },
   )
}
 }
}
</script>

<style>
 .map {
   position: absolute;
   margin-top: 50px;
   width: 400px !important;
   height: 400px !important;
   overflow :hidden
 }
</style>