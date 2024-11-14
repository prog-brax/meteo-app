<template>
  <q-input standout v-model="latitude" label="Latitude" />
  <q-input standout v-model="longitude" label="Longitude" />
  <q-btn color="amber" glossy label="Afficher" @click="searchMeteo" />
  <meteo-card
    v-for="(code, index) in Codes"
    :key="index"
    :codesReference="codesReference"
    :code="code"
  />
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import codes from "src/data/wmo-codes-fr.json";

import MeteoCard from 'src/components/MeteoCard.vue'

defineOptions({
  name: "IndexPage",
});

const meteoD = ref("");
const imageD = ref();
const Codes = ref([]);
const codesReference = ref(codes);
const latitude = ref("40");
const longitude = ref("2");

onMounted(async () => {
  searchMeteo();
});

async function searchMeteo() {
  const meteo = await axios.get(
    "https://api.open-meteo.com/v1/forecast?latitude=" +
      latitude.value +
      "&longitude=" +
      longitude.value +
      "&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,uv_index_clear_sky_max&current=weather_code"
  );
  const etat = meteo.data.current.weather_code;
  Codes.value = meteo.data.daily.weather_code;
  imageD.value = codes[etat].day.image;
  meteoD.value = codes[etat].day.description;
}

</script>
