<script setup lang="ts">
import { computed, reactive } from 'vue';

const state = reactive<{
  start: number;
  last: number;
  length: number;
  count: number
}>({
  start: 0,
  last: 0,
  length: 2.0,
  count: 0
})

const speed = computed(() => {
  const hours = (state.last - state.start) / (1000 * 3600);
  const km = state.count * state.length / 1000;

  const speed = km/hours;
  return Math.round(speed * 100) / 100;
})

const trigger = () => {
  const now = Date.now();
  if (state.start === 0) {
    state.start = now; 
  } else {
    state.count++;
  }
  state.last = now;
}

const reset = () => {
  state.count = 0;
  state.start = 0;
}
</script>

<template>
  <div>
    <div>
      <input type="text" v-model.number="state.length">
    </div>
    <div>{{ speed }} km/h</div>
    <button @click="trigger">Trigger</button>
    <button @click="reset">Reset</button>
  </div>
</template>
