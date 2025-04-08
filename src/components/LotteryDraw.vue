<template>
  <div class="p-6 bg-gray-800 rounded-lg shadow-lg text-white text-center">
    <h2 class="text-2xl font-bold mb-4">Lottó Szimulátor</h2>

    <div class="mb-4">
      <h3 class="text-xl font-semibold">Adj meg 5 számot (1-90 között, ne ismétlődjenek)</h3>
      <div class="flex justify-center gap-2 mt-2">
        <input
          v-for="(num, index) in userNumbers"
          :key="index"
          v-model.number="userNumbers[index]"
          type="number"
          min="1"
          max="90"
          inputmode="numeric"
          pattern="[0-9]*"
          class="w-12 h-12 text-center rounded bg-gray-700 text-white no-spinner"
          :disabled="useRandomNumbers"
          @input="validateInput(index)"
        />
      </div>
      <button @click="toggleRandomMode" class="mt-2 px-3 py-1 bg-yellow-500 rounded text-black">
        {{ useRandomNumbers ? "Saját számok használata" : "Véletlenszerű számok használata" }}
      </button>
    </div>

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

    <div class="mt-6">
      <h3 class="text-xl font-semibold">Találati statisztika</h3>
      <p class="text-sm">2 találatos: {{ matchStats[2] }} db</p>
      <p class="text-sm">3 találatos: {{ matchStats[3] }} db</p>
      <p class="text-sm">4 találatos: {{ matchStats[4] }} db</p>
      <p class="text-sm">5 találatos (Főnyeremény!): {{ matchStats[5] }} db</p>
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
import { ref } from "vue";

const drawnNumbers = ref([]);
const userNumbers = ref([1, 2, 3, 4, 5]);
const speed = ref(500);
const isDrawing = ref(false);
const useRandomNumbers = ref(false);
const matchStats = ref({ 2: 0, 3: 0, 4: 0, 5: 0 });
let intervalId = null;

const randomizeNumbers = () => {
  const randomSet = new Set();
  while (randomSet.size < 5) {
    randomSet.add(Math.floor(Math.random() * 90) + 1);
  }
  userNumbers.value = [...randomSet];
};

const drawNumbers = () => {
  const numbers = new Set();
  while (numbers.size < 5) {
    numbers.add(Math.floor(Math.random() * 90) + 1);
  }
  drawnNumbers.value = [...numbers];

  if (useRandomNumbers.value) {
    randomizeNumbers();
  }

  const matches = drawnNumbers.value.filter(num => userNumbers.value.includes(num)).length;
  if (matches >= 2) {
    matchStats.value[matches]++;
  }
};

const toggleRandomMode = () => {
  useRandomNumbers.value = !useRandomNumbers.value;
  if (useRandomNumbers.value) {
    randomizeNumbers();
  } else {
    userNumbers.value = [1, 2, 3, 4, 5];
  }
};

const validateInput = (index) => {
  let value = userNumbers.value[index];

  if (value < 1) userNumbers.value[index] = 1;
  if (value > 90) userNumbers.value[index] = 90;
  if (isNaN(value)) userNumbers.value[index] = null;

  const uniqueNumbers = new Set(userNumbers.value);
  if (uniqueNumbers.size < userNumbers.value.length) {
    userNumbers.value[index] = null;
  }
};

const toggleDraw = () => {
  const uniqueNumbers = new Set(userNumbers.value);

  if (uniqueNumbers.size < userNumbers.value.length) {
    alert("Nem indítható a sorsolás, mert ismétlődő számokat adtál meg!");
    return;
  }

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

<style>
.no-spinner::-webkit-outer-spin-button,
.no-spinner::-webkit-inner-spin-button {
  appearance: none;
  margin: 0;
}
.no-spinner {
  appearance: none;
}
</style>
