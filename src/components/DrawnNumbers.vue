<template>
  <div class="mt-6">
    <h3 class="text-xl font-semibold">Kihúzott számok</h3>
    <div class="flex justify-center gap-4 mt-2">
      <div
        v-for="num in drawnNumbers"
        :key="num"
        class="w-12 h-12 flex items-center justify-center bg-blue-500 rounded-full text-lg font-bold"
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
