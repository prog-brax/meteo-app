<template>
    <q-card class="my-card">
    <img
      :src="codesReference[code].day.image"
      height="100"
      style="width: 100px"
    />
    <q-card-section>
      <div class="text-h6">{{ codesReference[code].day.description }}</div>
      <div class="text-subtitle2">by me</div>
    </q-card-section>
    <q-card-section class="q-pt-none">
      {{ lorem }}
    </q-card-section>
  </q-card>
</template>

<script setup>
defineProps({
  codesReference: Object,
  code: Number,
})

</script>
