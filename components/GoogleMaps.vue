<template>
  <div>
    <div ref="map" class="g-map"></div>
  </div>
</template>

<script>
import { Loader } from "@googlemaps/js-api-loader";

export default {
  mounted() {
    this.loadGoogleMaps();
  },
  methods: {
    loadGoogleMaps() {
      const loader = new Loader({
        apiKey: process.env.GOOGLE_MAPS_API_KEY,
        version: "weekly",
      });

      loader.load().then(() => {
        this.initMap();
      });
    },
    initMap() {
      const map = new google.maps.Map(this.$refs.map, {
        center: { lat: 37.7749, lng: -122.4194 },
        zoom: 7,
      });

      // Add your custom map functionality here
    },
  },
};
</script>

<style scoped>
.g-map {
  width: 500px;
  height: 500px;
}

</style>
