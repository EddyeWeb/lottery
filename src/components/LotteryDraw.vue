<template>
  <div class="p-6 bg-gray-800 rounded-lg shadow-lg text-white text-center">
    <h2 class="text-2xl font-bold mb-4">Kihúzott számok</h2>
    <div class="flex justify-center gap-4">
      <div
        v-for="num in drawnNumbers"
        :key="num"
        class="w-12 h-12 flex items-center justify-center bg-blue-500 rounded-full text-lg font-bold"
      >
        {{ num }}
      </div>
    </div>

    <div class="mt-6">
      <label for="speed" class="block text-sm font-medium">Sorsolási sebesség</label>
      <input
        id="speed"
        type="range"
        min="1"
        max="1000"
        v-model="speed"
        class="w-full mt-2"
        @input="updateSpeed"
      />
      <p class="mt-2 text-sm">Sebesség: {{ speed }} ms</p>
    </div>

    <button @click="toggleDraw" class="mt-4 px-4 py-2 bg-green-500 rounded text-white">
      {{ isDrawing ? "Sorsolás leállítása" : "Sorsolás indítása" }}
    </button>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const drawnNumbers = ref([]);
const speed = ref(500);
const isDrawing = ref(false);
let intervalId = null;

const drawNumbers = () => {
  const numbers = new Set();
  while (numbers.size < 5) {
    numbers.add(Math.floor(Math.random() * 90) + 1);
  }
  drawnNumbers.value = [...numbers];
};

const toggleDraw = () => {
  if (isDrawing.value) {
    clearInterval(intervalId);
    isDrawing.value = false;
  } else {
    isDrawing.value = true;
    intervalId = setInterval(drawNumbers, speed.value);
  }
};

const updateSpeed = () => {
  if (isDrawing.value) {
    clearInterval(intervalId);
    intervalId = setInterval(drawNumbers, speed.value);
  }
};
</script>
