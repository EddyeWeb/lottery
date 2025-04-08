<template>
  <div class="mt-6">
    <h3 class="text-xl font-semibold">Eltelt idő</h3>
    <p class="text-sm">{{ years }} év</p>
  </div>
</template>

<script setup>
const props = defineProps({
  years: Number
});
</script>
