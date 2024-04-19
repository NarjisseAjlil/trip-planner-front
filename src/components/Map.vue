<!-- src/components/Map.vue -->

<template>
  <div id="map"></div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
const data = ref();
const mapLocations = ref([]);
const map = ref();

onMounted(async () => {
  const route = useRoute();
  const id = route.params.id;
  map.value = L.map("map").setView([51.505, -0.09], 13);
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution:
      'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
  }).addTo(map.value);
  const response = await fetch(`http://localhost:3000/v1/trips/${id}`);
  const jsonAnswer = await response.json();

  data.value = jsonAnswer;
  mapLocations.value = jsonAnswer.output;
  const markers = mapLocations.value.map((mapPoint) => {
    return L.marker([
      mapPoint.location.latitude,
      mapPoint.location.longitude,
    ]).addTo(map.value);
  });
  const group = L.featureGroup(markers);
  map.value.fitBounds(group.getBounds());
});
</script>

<style scoped>
#map {
  height: 400px;
}
</style>
