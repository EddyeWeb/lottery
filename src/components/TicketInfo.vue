<template>
  <div class="ticket-info">
    <p class="text-sm">Number of tickets: {{ ticketCount }}</p>
    <p class="text-sm">Years spent: {{ years }}</p>
    <p class="text-sm">Cost of tickets: {{ totalCost }} Ft</p>
  </div>
</template>

<script setup>
const props = defineProps({
  ticketCount: Number,
  years: Number,
  totalCost: Number
});
</script>
