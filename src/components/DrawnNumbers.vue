<template>
  <div class="number-output">
    <div class="flex flex-wrap items-center gap-2 mt-2">
      <p class="w-full md:w-auto">Winning numbers:</p>
      <div
        v-for="num in drawnNumbers"
        :key="num"
        class="w-12 h-12 text-center mb-2 md:mb-0"
      >
        {{ num }}
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  drawnNumbers: Array
});
</script>
