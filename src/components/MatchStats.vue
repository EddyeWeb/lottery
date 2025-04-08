<template>
  <div class="matches flex">
    <div class="text-center">
      <p class="text-sm">2 matches:</p>
      <p> {{ matchStats[2] }}</p>
    </div>
    <div class="text-center">
      <p class="text-sm">3 matches:</p>
      <p> {{ matchStats[3] }}</p>
    </div>
    <div class="text-center">
      <p class="text-sm">4 matches:</p>
      <p> {{ matchStats[4] }}</p>
    </div>
    <div class="text-center">
      <p class="text-sm">5 matches:</p>
      <p> {{ matchStats[5] }}</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  matchStats: Object
});
</script>
