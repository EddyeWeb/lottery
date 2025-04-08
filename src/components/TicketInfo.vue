<template>
  <div class="ticket-info bg-blue-500">
    <div>
      <p><strong><span>Number of tickets:</span> {{ ticketCount }}</strong></p>
    </div>
    <div>
      <p><span>Years spent:</span> {{ years }}</p>
    </div>
    <div>
      <p><span>Cost of tickets:</span> {{ totalCost }} Ft</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  ticketCount: Number,
  years: Number,
  totalCost: Number
});
</script>
