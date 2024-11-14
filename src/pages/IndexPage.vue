<template>
  <q-page class="flex flex-center">
    <q-card class="my-card">
      <img :src="tempsImage">

      <q-card-section>
        <div class="text-h6">Météo du jour</div>
        <div class="text-subtitle2">{{ temps }}</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        {{ lorem }}
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'

import axios from 'axios'

import wmoCodes from 'src/data/wmo-codes-fr.json'

defineOptions({
  name: 'IndexPage',
})

const temps = ref('')
const tempsImage =ref('')

const currentMeteo = ref(null)
const dailyMeteo = ref(null)

onMounted(async () => {
  const meteoResults = await axios.get(`https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&current=temperature_2m,relative_humidity_2m,apparent_temperature,precipitation,rain,weather_code&daily=weather_code,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min`)

  currentMeteo.value = meteo.data.current
  dailyMeteo.value = meteo.data.daily



  temps.value = wmoCodes[code].day.description
  tempsImage.value = wmoCodes[code].day.image
})

</script>
