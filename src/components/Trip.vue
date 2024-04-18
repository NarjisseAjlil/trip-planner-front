<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const trip = ref({});

const route = useRoute();
const id = route.params.id;

onMounted(async () => {
  const response = await fetch(`http://localhost:3000/v1/trips/${id}`);
  trip.value = await response.json();
});
</script>

<template>
  <div>
    <h1>{{ trip.prompt }}</h1>
    <h2>Itinéraire</h2>
    <ol class="individual-trip" v-for="location in trip.output">
      <li>
        <p>{{ location.name }}</p>
      </li>
      <p>{{ location.description }}</p>
    </ol>
  </div>
</template>
