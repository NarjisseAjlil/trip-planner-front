<!-- src/components/Trip.vue -->

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import { SquarePen } from "lucide-vue-next";

const trip = ref({});

const route = useRoute();
const id = route.params.id;

onMounted(async () => {
  const response = await fetch(`http://localhost:3000/v1/trips/${id}`);
  trip.value = await response.json();
});
</script>

<template>
  <div style="margin: 5%">
    <div class="trip-container">
      <p class="trip-prompt">
        {{ trip.prompt }}
      </p>
      <SquarePen />
    </div>

    <p style="color: #958f7e; font-family: Inter; font-weight: 500">
      Itinéraire
    </p>
    <ol class="individual-trip" v-for="location in trip.output">
      <li>
        <p class="location-name">{{ location.name }}</p>
      </li>
      <p>{{ location.description }}</p>
    </ol>
  </div>
</template>
