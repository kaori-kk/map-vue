<template>
  <div id="map" style="width:700px; height:500px"></div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import mapboxgl, { MapboxOptions, Map } from 'mapbox-gl'

@Component({})
export default class extends Vue {
  map: Map = {} as Map
  option: MapboxOptions = {
    accessToken: 'pk.eyJ1Ijoia2sta2FvcmkiLCJhIjoiY2s2YzY4d2VhMTVnYTNqcWpqcG0xaDBkMSJ9.PjJTu6RvJVQPqrT_CSUGFQ',
    container: 'map',
    style: 'mapbox://styles/kk-kaori/ckbrxmui90lc11ilzmyv5vwzm',
    center: [143.767125, 38.681236],
    zoom: 2
  }

  mounted() {
    this.map = new mapboxgl.Map(this.option)
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
  margin: 0;
  padding: 0;
}

#map {
  margin: 0 auto;
}
</style>
