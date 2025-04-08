<template>
  <div class="mt-6">
    <label for="speed" class="block text-sm font-medium">Sorsolási sebesség</label>
    <input
      id="speed"
      type="range"
      min="1"
      max="1000"
      :value="speed"
      @input="onInput"
      class="w-full mt-2"
    />
    <p class="mt-2 text-sm">Sebesség: {{ internalSpeed }} ms</p>
  </div>
</template>

<script setup>
import { watch, ref } from 'vue';

const emit = defineEmits(['update-speed']);
const props = defineProps({ speed: Number });

const onInput = (e) => {
  emit('update-speed', Number(e.target.value));
};

watch(() => props.speed, val => {
  internalSpeed.value = val;
});
</script>
