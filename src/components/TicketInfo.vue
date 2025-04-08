<template>
  <div class="mt-6">
    <h3 class="text-xl font-semibold">Szelvények és költség</h3>
    <p class="text-sm">Feladott szelvények száma: {{ ticketCount }}</p>
    <p class="text-sm">Összes költség: {{ totalCost }} Ft</p>
  </div>
</template>

<script setup>
const props = defineProps({
  ticketCount: Number,
  totalCost: Number
});
</script>
