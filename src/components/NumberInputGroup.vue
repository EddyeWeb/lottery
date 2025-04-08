<template>
  <div class="mb-4">
    <h3 class="text-xl font-semibold">Számaim</h3>
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
        @input="$emit('validate', index)"
      />
    </div>
    <button @click="$emit('toggle-random')" class="mt-2 px-3 py-1 bg-yellow-500 rounded text-black">
      {{ useRandomNumbers ? "Saját számok használata" : "Véletlenszerű számok használata" }}
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
