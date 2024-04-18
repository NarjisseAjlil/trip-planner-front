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
  <p class="last-trips">Derniers itinéraires</p>
  <div class="trips">
    <p class="trip" v-for="item in data">
      {{ item.prompt }}
    </p>
  </div>
</template>
