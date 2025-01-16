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
          </q-item-label>
            <q-list>
      <q-item>
        <q-item-section side>
          <q-item-label style="margin-top:35px;background-color:lightgrey">{{daily.temparatureMin}}</q-item-label>
        </q-item-section>
            <q-item-section avatar>
        <q-img src="/images/meteo-min-max.png" />
      </q-item-section>
      
      <q-item-section>
          <q-item-label>{{daily.temperatureMax}}</q-item-label>
        </q-item-section>
</q-item></q-list>
          
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
