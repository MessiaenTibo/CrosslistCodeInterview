<script setup>
import { computed, onMounted, ref } from 'vue'
import InputField from '@/components/InputField.vue'
// Words
let allWorldList = ref([])
let puzzelWorldList = ref([])
let randomWord = ref('')

// Guesses
let guesse = ''
let guesseCount = 0
const maxGuesseLenght = 5
const maxGuesses = 6

function getAllWorlds() {
  fetch('https://api-334903298972.us-central1.run.app/alle_woorden')
    .then((res) => res.json())
    .then((data) => {
      allWorldList.value = data.alle_woorden
    })
  fetch('https://api-334903298972.us-central1.run.app/puzzel_woorden')
    .then((res) => res.json())
    .then((data) => {
      puzzelWorldList.value = data.puzzel_woorden
      randomWord.value =
        puzzelWorldList.value[
          Math.floor(Math.random() * puzzelWorldList.value.length)
        ]
      console.log(randomWord.value)
    })
}
getAllWorlds()

onMounted(() => {
  function checkGuessedWord() {
    if (guesse.length == maxGuesseLenght) {
      // Check if guesse is in the all words list
      if (!allWorldList.value.includes(guesse)) {
        console.log('not a word')
        return
      }

      const letters = [...guesse]
      // console.log(letters)
      // check each letter if it is in the word
      let correct = []
      let wrong = []
      let wrongPlace = []
      for (let i = 0; i < letters.length; i++) {
        if (randomWord.value.includes(letters[i])) {
          if (randomWord.value[i] == letters[i]) {
            correct.push(letters[i])
          } else {
            wrongPlace.push(letters[i])
          }
        } else {
          wrong.push(letters[i])
        }
      }
      console.log('correct', correct)
      console.log('wrong', wrong)
      console.log('wrongPlace', wrongPlace)

      // reset guesse
      guesseCount++
      guesse = ''
      console.log('Guesses left:', maxGuesses - guesseCount)
      if (guesseCount == maxGuesses) {
        console.log('game over')
      }
    } else {
      console.log('not enough letters')
    }
  }
  // register keydown event
  window.addEventListener('keydown', (e) => {
    if (e.key == 'Enter') {
      checkGuessedWord()
    } else if (guesse.length < maxGuesseLenght) {
      guesse += e.key
      console.log(guesse)
    }
  })
})
</script>

<template>
  <main class="flex flex-col items-center justify-center h-screen">
    <div class="grid grid-cols-5 gap-1 w-fit">
      <!-- row 1 -->
      <InputField />
      <InputField guesse="wrong" />
      <InputField guesse="wrong-place" />
      <InputField guesse="correct" />
      <InputField />
      <!-- row 2 -->
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <!-- row 3 -->
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <!-- row 4 -->
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <!-- row 5 -->
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <!-- row 6 -->
      <InputField />
      <InputField />
      <InputField />
      <InputField />
      <InputField />
    </div>
  </main>
</template>
