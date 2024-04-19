<!-- src/components/ListHistory.vue -->

<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";

const data = ref([]);
const router = useRouter();

// call api
onMounted(async () => {
  const response = await fetch("http://localhost:3000/v1/trips");
  data.value = await response.json();
});

const goToTrip = (id) => {
  router.push(`/trips/${id}`);
};
</script>

<template>
  <div class="history-list-trips">
    <p class="last-trips">Derniers itinéraires</p>

    <p
      class="list-history-trip"
      v-for="item in data"
      @click="goToTrip(item.id)"
    >
      {{ item.prompt }}
      <img src="../assets/arrow.png" alt="" />
    </p>
  </div>
</template>
