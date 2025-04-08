<template>
  <div class="mt-6">
    <h3 class="text-xl font-semibold">Találati statisztika</h3>
    <p class="text-sm">2 találatos: {{ matchStats[2] }} db</p>
    <p class="text-sm">3 találatos: {{ matchStats[3] }} db</p>
    <p class="text-sm">4 találatos: {{ matchStats[4] }} db</p>
    <p class="text-sm">5 találatos (Főnyeremény!): {{ matchStats[5] }} db</p>
  </div>
</template>

<script setup>
const props = defineProps({
  matchStats: Object
});
</script>
