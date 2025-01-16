<template>
  <q-input outlined bottom-slots v-model="cityToSearch" label="Quelle ville voulez-vous rentrer?" 
  @keydown.enter.prevent="searchCity"
  >
    <template v-slot:prepend>
      <q-icon name="place" />
    </template>
    <template v-slot:append>
      <q-icon name="close" @click="cityToSearch = ''" class="cursor-pointer"/>
    </template>
  </q-input>
  <q-btn color= "amber" @click="searchCity"> Chercher</q-btn>
  <meteo-card
    v-for="(dailyMeteo, index) in daily"
    :key="index"
    :codesReference="codesReference"
    :daily="dailyMeteo"
  />
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import codes from "src/data/wmo-codes-fr.json";

import MeteoCard from "src/components/MeteoCard.vue";

defineOptions({
  name: "IndexPage",
});

const meteoD = ref("");
const imageD = ref();
const Codes = ref([]);
const daily = ref([]);
const codesReference = ref(codes);
const latitude = ref("40");
const longitude = ref("2");
const cityToSearch = ref('')

onMounted(async () => {
  searchMeteo();
});

async function searchCity() {
  const villes = await axios.get(`https://api.openweathermap.org/geo/1.0/direct?q=${cityToSearch.value}&appid=e0c7fc36e50292f9b00704bd4eede937`)
  longitude.value = villes.data[0].lon
  latitude.value = villes.data[0].lat
  searchMeteo()
}

async function searchMeteo() {
  const meteo = await axios.get(
    "https://api.open-meteo.com/v1/forecast?latitude=" +
      latitude.value +
      "&longitude=" +
      longitude.value +
      "&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max,uv_index_clear_sky_max&current=weather_code",
  );
  const etat = meteo.data.current.weather_code;
  console.log(meteo.data.daily);
  Codes.value = meteo.data.daily.weather_code;
  imageD.value = codes[etat].day.image;
  meteoD.value = codes[etat].day.description;
  const time = meteo.data.daily.time;
  daily.value = [];
  for (let index = 0; index < time.length; index++) {
    daily.value.push({
      time: time[index],
      temperatureMax: meteo.data.daily.temperature_2m_max[index],
      temparatureMin: meteo.data.daily.temperature_2m_min[index],
      weatherCode: meteo.data.daily.weather_code[index],
    });
  }
}
</script>
