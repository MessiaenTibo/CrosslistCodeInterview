<!-- Input field for a woordle letter -->
<script setup>
import { ref } from 'vue'
const props = defineProps({
  guesse: String, // empty or wrong or wrong-place or correct
})

let letter = ref('')
</script>

<template>
  <input
    :class="`border w-20 h-20  text-black text-4xl text-center font-semibold capitalize ${
      guesse == 'wrong'
        ? 'bg-gray-500 text-white '
        : guesse == 'wrong-place'
        ? 'bg-yellow-500 text-white '
        : guesse == 'correct'
        ? 'bg-green-500 text-white '
        : ''
    }${letter.length == 0 ? '' : 'bg-gray-300'}`"
    type="text"
    maxlength="1"
    v-model="letter"
  />
</template>
