<template>
  <div>
    {{ msg }}
    <div id="map" />
  </div>
</template>

<script lang="ts">
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";

import { defineComponent, onMounted, reactive } from "vue";
export default defineComponent({
  name: "HelloWorld",
  props: { msg: String },
  setup(props, context) {
    const mapstyle = reactive<mapboxgl.Style>({
      version: 8,
      sources: {
        OSM: {
          type: "raster",
          tiles: ["http://tile.openstreetmap.org/{z}/{x}/{y}.png"],
          tileSize: 256,
          attribution:
            '<a href="http://osm.org/copyright">© OpenStreetMap contributors</a>',
        },
      },
      layers: [
        {
          id: "OSM",
          type: "raster",
          source: "OSM",
          minzoom: 0,
          maxzoom: 18,
        },
      ],
    });
    onMounted(() => {
      const map = new mapboxgl.Map({
        container: "map",
        style: mapstyle,
        center: [140.0, 38.2],
        zoom: 9,
        maxZoom: 18,
      });
    });
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map {
  height: 1000px;
}
</style>
