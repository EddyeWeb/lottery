<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white">
    <h1 class="text-3xl font-bold mb-6">Lottó Szimulátor</h1>
    <LotteryDraw />
  </div>
</template>

<script setup>
import LotteryDraw from "./components/LotteryDraw.vue";
</script>
