<template>
  <div class="lottery-base bg-white text-black max-w-full">
    <h1>
      Result
    </h1>

    <TicketInfo :ticket-count="ticketCount" :years="elapsedYears" :total-cost="totalCost" />

    <MatchStats :match-stats="matchStats" />

    <NumberInputGroup
      :user-numbers="userNumbers"
      :use-random-numbers="useRandomNumbers"
      @toggle-random="toggleRandomMode"
      @validate="validateInput"
    />

    <DrawnNumbers :drawn-numbers="drawnNumbers" />

    <div class="mt-6">
      <p class="mt-2 text-sm">Speed: {{ speed }} ms</p>
      <input
        id="speed"
        type="range"
        min="1"
        max="1000"
        v-model="speed"
        class="w-full mt-2"
        @input="updateSpeed"
      />
    </div>

    <button @click="toggleDraw" class="mt-4 px-4 py-2 bg-green-500 rounded text-white">
      {{ isDrawing ? "Sorsolás leállítása" : "Sorsolás indítása" }}
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import NumberInputGroup from "./NumberInputGroup.vue";
import DrawnNumbers from "./DrawnNumbers.vue";
import MatchStats from "./MatchStats.vue";
import TicketInfo from "./TicketInfo.vue";

const drawnNumbers = ref([]);
const userNumbers = ref([1, 2, 3, 4, 5]);
const speed = ref(500);
const isDrawing = ref(false);
const useRandomNumbers = ref(false);
const matchStats = ref({ 2: 0, 3: 0, 4: 0, 5: 0 });
const ticketCount = ref(0);
const totalCost = ref(0);
const elapsedYears = ref(0);
const ticketPrice = 300;
const weeksInYear = 52;
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
    matchStats.value = {
      ...matchStats.value,
      [matches]: matchStats.value[matches] + 1
    };
  }

  ticketCount.value++;
  totalCost.value = ticketCount.value * ticketPrice;
  elapsedYears.value = Math.floor(ticketCount.value / weeksInYear);

  if (matches === 5) {
    clearInterval(intervalId);
    isDrawing.value = false;
    alert(`Gratulálunk! Megnyerted az 5 találatos főnyereményt ${elapsedYears.value} év alatt!`);
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
</script>
