<script setup lang="ts">
import { ref } from 'vue';
const count = ref(0);

const increment = () => {
  count.value++;
};
</script>

<template>
  <h1 class="text-2xl text-gray-950 font-semibold">Hello World</h1>
  <p>Counter {{ count }}</p>
  <button @click="increment" class="border w-20">Add</button>
</template>
