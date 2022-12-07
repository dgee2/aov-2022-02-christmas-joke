<template>
  <div class="w-full h-full flex flex-col justify-center items-center">
    <div class="text-3xl" v-if="jokeState !== 'gettingJoke'">{{ jokeSetup }}</div>
    <div class="text-3xl" v-if="jokeState === 'answer'">{{ jokeResponse }}</div>
    <button
      class="px-4 py-2 font-semibold text-sm bg-cyan-500 text-white rounded-full shadow-sm"
      @click="getAnswer()"
      v-if="jokeState === 'newJoke'"
    >
      Tell Me!
    </button>
    <button
      class="px-4 py-2 font-semibold text-sm bg-cyan-500 text-white rounded-full shadow-sm"
      @click="getNewJoke()"
      v-if="jokeState === 'answer'"
    >
      New Joke
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const jokeState = ref('gettingJoke')

async function getNewJoke() {
  jokeState.value = 'gettingJoke'
  const result = await (await fetch('https://v2.jokeapi.dev/joke/christmas')).json()
  jokeSetup.value = result.setup
  jokeResponse.value = result.delivery
  jokeState.value = 'newJoke'
}

function getAnswer() {
  jokeState.value = 'answer'
}

const jokeSetup = ref('')
const jokeResponse = ref('')

getNewJoke()
</script>
