<template>
<div>
  <input type="text" placeholder='Type Country Name...' v-model='query' @keypress='fetchMap'>
  <MglMap
    :accessToken="accessToken"
    :mapStyle.sync ="mapStyle"
    :center="center"
    :zoom="zoom"
  >
    <div v-for="(coordinate, index) in coordinates" :key="index">
      <MglMarker :coordinates="[coordinate.lng, coordinate.lat]" color="blue"/>
    </div>
  </MglMap>
</div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { MglMap, MglMarker } from "vue-mapbox";
import Mapbox from "mapbox-gl";

@Component({
  components: {
    MglMap,
    MglMarker
  }
})

export default class extends Vue {
  base_url = 'https://api.mapbox.com/geocoding/v5/mapbox.places/'
  query = ''
  accessToken ='pk.eyJ1Ijoia2sta2FvcmkiLCJhIjoiY2s2YzY4d2VhMTVnYTNqcWpqcG0xaDBkMSJ9.PjJTu6RvJVQPqrT_CSUGFQ'
  mapStyle = 'mapbox://styles/kk-kaori/ckbrxmui90lc11ilzmyv5vwzm'
  center = [143.767125, 38.681236]
  zoom = 2
  coordinates = []

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  }

  fetchMap(e: any){
    if(e.key == 'Enter'){
      fetch(`${this.base_url}${this.query}.json?limit=1&access_token=${this.accessToken}`)
      .then(res => {
        return res.json();
      }).then(data => {
        const coordinates = {lng: data.features[0].center[0], lat: data.features[0].center[1]}
        this.coordinates.push(coordinates);
        console.log(this.coordinates)
        this.query = "";
      })
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  @import 'mapbox-gl/dist/mapbox-gl';

  *{
  margin: 0;
  padding: 0;
}

#map {
  margin: 0 auto;
}

.mgl-map-wrapper {
  height: 500px;
}

</style>

