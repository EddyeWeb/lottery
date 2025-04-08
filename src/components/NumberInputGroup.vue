<template>
  <div class="number-input">
    <div class="flex flex-wrap items-center gap-2 mt-4 mb-4">
      <p class="w-full md:w-auto">Your numbers:</p>
      <input
        v-for="(num, index) in userNumbers"
        :key="index"
        v-model.number="userNumbers[index]"
        type="number"
        min="1"
        max="90"
        inputmode="numeric"
        pattern="[0-9]*"
        class="w-12 h-12 text-center no-spinner mb-2 md:mb-0"
        :disabled="useRandomNumbers"
        @input="$emit('validate', index)"
      />
    </div>
    <button
      @click="$emit('toggle-random')"
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4"
    >
      {{ useRandomNumbers ? "Play with personal numbers" : "Play with random numbers" }}
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  userNumbers: Array,
  useRandomNumbers: Boolean
});
const emit = defineEmits(['toggle-random', 'validate']);
</script>

<style scoped>
.no-spinner::-webkit-outer-spin-button,
.no-spinner::-webkit-inner-spin-button {
  appearance: none;
  margin: 0;
}
.no-spinner {
  appearance: none;
}
</style>
