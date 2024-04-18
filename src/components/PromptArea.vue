<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const data = ref([]);
const prompt = ref();
const router = useRouter();

async function sendData() {
  const response = await fetch("http://localhost:3000/v1/trips", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ prompt: prompt.value }),
  });
  const responseData = await response.json();
  console.log(responseData);
  return responseData.id;
}

const sendSubmit = async (event) => {
  const id = await sendData();
  router.push(`trips/${id}`);
};
</script>

<template>
  <h1 class="title">
    Planificateur <br />
    de voyages
  </h1>
  <p class="subtitle">généré par IA</p>
  <form @submit.prevent="sendSubmit">
    <div class="input-container">
      <input type="text" class="input" v-model="prompt" />
    </div>

    <div class="button-container">
      <button class="start-button" type="submit">C'est parti !</button>

      <button class="example-button">Voir un exemple</button>
    </div>
  </form>
</template>
