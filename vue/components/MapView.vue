<template>
  <div ref="mapWrapper" class="map-wrapper"></div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import L from "leaflet";

const props = defineProps<{
  data: Array<any>,
}>()

    const { data } = props;
    const mapWrapper = ref(null);
    const iconUrl = new URL("../../images/map-marker.png", import.meta.url);

    onMounted(() => {
      if (!data) return;

      const map = L.map(mapWrapper.value, {
        scrollWheelZoom: false,
        maxZoom: 15,
        center: [51.39505310626257, 1.5496942960543323],
        zoom: 10,
      });

      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 15,
        attribution:
          '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
      }).addTo(map);

      const icon = L.icon({
        iconUrl,
        iconSize: [34, 38],
        iconAnchor: [17, 38],
      });

      data.map((d) => {
        L.marker([d.lat, d.long], {
          icon,
        }).addTo(map);
      });
    });
</script>

<style scoped>
@import "../../node_modules/leaflet/dist/leaflet.css";

.map-wrapper {
  aspect-ratio: 16 / 9;
}
</style>
