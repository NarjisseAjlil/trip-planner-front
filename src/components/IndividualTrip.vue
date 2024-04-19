<!-- src/components/IndividualTrip.vue -->

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const trip = ref({});

const route = useRoute();
const id = route.params.id;

// call api
onMounted(async () => {
  const response = await fetch(`http://localhost:3000/v1/trips/${id}`);
  trip.value = await response.json();
});
</script>

<template>
  <div class="individual-trip">
    <div class="individual-trip-container">
      <p class="individual-trip-prompt">
        {{ trip.prompt }}
      </p>
    </div>

    <p style="color: #958f7e; font-family: Inter; font-weight: 500">
      Itinéraire
    </p>
    <ol class="individual-trip-description">
      <li v-for="location in trip.output">
        <p class="location-name">{{ location.name }}</p>
        <p>{{ location.description }}</p>
      </li>
    </ol>
  </div>
</template>
