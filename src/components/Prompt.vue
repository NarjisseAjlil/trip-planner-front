<script setup>
import { ref, onMounted } from "vue";
import { Icon } from "@iconify/vue";

const data = ref([]);

onMounted(async () => {
  const response = await fetch("http://localhost:3000/v1/trips");
  data.value = await response.json();
});
</script>

<template>
  <h1 class="title">
    Planificateur <br />
    de voyages
  </h1>
  <p class="subtitle">généré par IA</p>

  <div class="input-container">
    <input type="text" class="input" />
  </div>

  <div class="button-container">
    <RouterLink to="/trips"
      ><button class="start-button">C'est parti !</button></RouterLink
    >

    <button class="example-button">Voir un exemple</button>
  </div>
</template>
