<!-- src/components/PromptArea.vue -->

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const data = ref([]);
const prompt = ref();
const router = useRouter();
const isLoading = ref(false);

// send data

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

// send submit

const sendSubmit = async (event) => {
  isLoading.value = true;
  const id = await sendData();
  router.push(`trips/${id}`);
  isLoading.value = false;
};
</script>

<template>
  <div class="compass">
    <img src="../assets/compass.png" alt="" />
  </div>
  <h1 class="title">
    Planificateur <br />
    de voyages
  </h1>
  <p class="subtitle">généré par IA</p>
  <form @submit.prevent="sendSubmit" v-if="!isLoading">
    <div class="input-container">
      <textarea type="text" class="input" v-model="prompt" />
    </div>

    <div class="button-container">
      <button class="start-button" type="submit">C'est parti !</button>

      <button class="example-button">Voir un exemple</button>
    </div>
  </form>

  <!-- Loader -->

  <div class="ui-abstergo" v-else="isLoading">
    <div class="abstergo-loader">
      <div></div>
      <div></div>
      <div></div>
    </div>
    <div class="ui-text">Création de votre voyage</div>
  </div>
</template>
