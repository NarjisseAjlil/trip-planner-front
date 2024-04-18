<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";

const data = ref([]);
const router = useRouter();

onMounted(async () => {
  const response = await fetch("http://localhost:3000/v1/trips");
  data.value = await response.json();
});

const goToTrip = (id) => {
  router.push(`/trips/${id}`);
};
</script>

<template>
  <p class="last-trips">Derniers itinéraires</p>
  <div class="trips">
    <p class="trip" v-for="item in data" @click="goToTrip(item.id)">
      {{ item.prompt }}
    </p>
  </div>
</template>
