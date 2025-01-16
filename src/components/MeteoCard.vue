<template>
  <div class="q-pa-md" style="max-width: 350px">
    <q-list bordered>
      <q-item clickable v-ripple>
        <q-item-section avatar>
          <img :src="codesReference[daily.weatherCode].day.image" />
        </q-item-section>
        <q-item-section>
          <q-item-label>
            <div class="text-h6">
              {{ daily.time }}
            </div>
          </q-item-label>
          <q-item-label caption>
            <div class="text-h6">
              {{ codesReference[daily.weatherCode].day.description }}
            </div>
            <div class="text-h6">
              {{ daily.temperatureMax }}°-{{ daily.temparatureMin }}°
            </div>
          </q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script setup>
defineProps({
  codesReference: Object,
  daily: Object,
});
</script>
