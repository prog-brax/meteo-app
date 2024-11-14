<template>
  <q-input standout v-model="latitude" label="Latitude" />
  <q-input standout v-model="longitude" label="Longitude" />
  <q-btn color="amber" glossy label="Afficher" @click="searchMeteo" />
  <q-card class="my-card" v-for="(Code, index) in Codes" :key="index">
    <img
      :src="codesReference[Code].day.image"
      height="100"
      style="width: 100px"
    />
    <q-card-section>
      <div class="text-h6">{{ codesReference[Code].day.description }}</div>
      <div class="text-subtitle2">by me</div>
    </q-card-section>
    <q-card-section class="q-pt-none">
      {{ lorem }}
    </q-card-section>
  </q-card>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import codes from "src/data/wmo-codes-fr.json";

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
