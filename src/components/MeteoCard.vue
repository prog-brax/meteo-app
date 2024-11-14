<template>
  <q-card class="my-card">
    <img
      :src="codesReference[daily.weatherCode].day.image"
      height="100"
      style="width: 100px"
    />
    <q-card-section>
      <div class="text-h6">
        {{ codesReference[daily.weatherCode].day.description }}
      </div>
      <div class="text-subtitle2">{{ daily.temperatureMax }}</div>
    </q-card-section>
    <q-card-section class="q-pt-none">
      {{ lorem }}
    </q-card-section>
  </q-card>
</template>

<script setup>
defineProps({
  codesReference: Object,
  daily: Object,
});
</script>
