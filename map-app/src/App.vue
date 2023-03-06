<template>
  <div id="map" />
</template>

<script>
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import { onMounted } from "vue";
export default {
  setup() {
    onMounted(() => {
      mapboxgl.accessToken =
        "pk.eyJ1IjoiZG11cnJheS1tdCIsImEiOiJjbGV2dTd6N2cwOHBnM3BudGluOXZmMmx2In0.BOEVpTFP8EZUsW8nz1e1lw";
      const map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/light-v9",
      });
      map.on('load', () => {
        map.addSource("usa", {
          type: "geojson",
          data:
            "https://raw.githubusercontent.com/johan/world.geo.json/master/countries/USA.geo.json",
        });
        map.addLayer({
          id: "usa-fill",
          type: "fill",
          source: "usa",
          paint: {
            "fill-color": "blue",
            "fill-opacity": .25
          },
        });
        map.on("click", "usa-fill", function (e) {
          new mapboxgl.Popup()
            .setLngLat(e.lngLat)
            .setHTML('Hello World.')
            .addTo(map);
        });
      });
    });
    return {};
  },
};
</script>

<style>
#map {
  height: 100vh;
}
</style>