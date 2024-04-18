<!-- src/components/ListHistory.vue -->

<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import { ChevronRight } from "lucide-vue-next";

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
  <p class="last-trips" style="margin: 5%; padding-top: 5%">
    Derniers itinéraires
  </p>
  <div class="trips">
    <p class="trip" v-for="item in data" @click="goToTrip(item.id)">
      {{ item.prompt }}
      <ChevronRight />
    </p>
  </div>
</template>
