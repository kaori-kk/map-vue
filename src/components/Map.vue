<template>
<div>
  <input type="text" placeholder='Type Country Name...' v-model='query' @keypress='fetchMap'>
  <MglMap
    :accessToken="accessToken"
    :mapStyle.sync ="mapStyle"
    :center="center"
    :zoom="zoom"
  >
  </MglMap>
    <!-- <MglMarker :coordinates="coordinates" color="blue" /> -->
</div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { MglMap, MglMarker } from "vue-mapbox";
import Mapbox from "mapbox-gl";
// import { MarkerOptions, LngLat, LngLatLike } from "mapbox-gl";

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

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  }

  fetchMap(e){
    if(e.key == 'Enter'){
      fetch(`${this.base_url}${this.query}.json?limit=1&access_token=${this.accessToken}`)
        .then(res => {
          return res.json();
        }).then(data => {
          console.log(data.features[0].center)
          //return 0 for longtitude, 1 for latitude
        })
    }
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
