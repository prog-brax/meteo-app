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
              {{ formattedDate }}
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
import { computed } from "vue";

import { format, parse } from "date-fns";
import { fr } from "date-fns/locale";

const props = defineProps({
  codesReference: Object,
  daily: Object,
});

const formattedDate = computed(() => {
  const date = parse(props.daily.time, "yyyy-MM-dd", new Date());
  return format(date, "eeee dd MMMM", { locale: fr });
});
</script>
