<template>
  <div id="map"></div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import L from "leaflet";
import "leaflet/dist/leaflet.css";

const prompt = ref("");
const key = "MAR8E5drMBTYVXle4Ohm";

onMounted(() => {
  const map = L.map("map", {
    center: L.latLng(0, 0), // Centre initial
    zoom: 5,
  });

  L.tileLayer(
    `https://api.maptiler.com/maps/streets-v2/{z}/{x}/{y}.png?key=${key}`,
    {
      tileSize: 512,
      zoomOffset: -1,
      minZoom: 1,
      attribution:
        '\u003ca href="https://www.maptiler.com/copyright/" target="_blank"\u003e\u0026copy; MapTiler\u003c/a\u003e \u003ca href="https://www.openstreetmap.org/copyright" target="_blank"\u003e\u0026copy; OpenStreetMap contributors\u003c/a\u003e',
      crossOrigin: true,
    }
  ).addTo(map);

  const updateMap = async () => {
    const locations = [
      { lat: 35.6895, lng: 139.6917, name: "Tokyo" },
      { lat: 34.6937, lng: 135.5023, name: "Kyoto" },
    ]; // Remplacez ceci par votre logique pour obtenir les emplacements de l'IA
    const bounds = L.latLngBounds();
    locations.forEach((location) => {
      const marker = L.marker([location.lat, location.lng]).addTo(map);
      marker.bindPopup(location.name);
      bounds.extend([location.lat, location.lng]);
    });
    map.fitBounds(bounds);
  };

  updateMap(); // Appelez la fonction une fois pour afficher les emplacements initiaux
});
</script>

<style scoped>
#map {
  height: 400px;
}
</style>
