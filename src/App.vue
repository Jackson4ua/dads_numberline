<script setup lang="ts">
import { ref } from 'vue'

const numbersList = ref<number[]>([])
const mysteryNum = ref(0)

for (let i = 1; i <= 100; i++) {
  numbersList.value.push(i)
}

function newNumber() {
  mysteryNum.value = Math.round(Math.random() * 100)
  for (let i = 1; i <= 100; i++) {
    const item = document.getElementById(`${i}-btn`)
    if (item) {
      const text = document.getElementById(`${i}-text`)
      text?.style.setProperty('visibility', 'hidden')
      if (item!.classList.contains('btn-success')) {
        item!.classList.remove('btn-success')
      }
      if (item!.classList.contains('btn-outline-danger')) {
        item!.classList.remove('btn-outline-danger')
      }
      item!.classList.add('btn-outline-primary')
    }
  }
}

function guessNumber(guess) {
  if (guess === mysteryNum.value) {
    document
      .getElementById(`${guess}-btn`)!
      .classList
      .remove('btn-outline-primary')

    document.getElementById(`${guess}-btn`)!.classList.add('btn-success')

    document
      .getElementById(`${guess}-text`)!
      .style
      .setProperty('visibility', 'visible')
  }
  else {
    document
      .getElementById(`${guess}-btn`)!
      .classList
      .remove('btn-outline-primary')

    document
      .getElementById(`${guess}-btn`)!
      .classList
      .add('btn-outline-danger')

    document
      .getElementById(`${guess}-text`)!
      .style
      .setProperty('visibility', 'visible')
  }
}

newNumber()
</script>

<template>
  <div class="d-flex flex-column justify-content-center align-items-center">
    <div class="m-1">
      <h2 class="display-2">
        Mr. Holbrook's Number Line
      </h2>
      <div class="d-flex justify-content-evenly">
        <h2 class="display-5">
          Find: {{ mysteryNum }}
        </h2>
        <button class="btn btn-primary" @click="newNumber()">
          New Number
        </button>
      </div>
    </div>
    <div
      class="d-flex flex-wrap justify-content-center align-items-center border rounded"
      style="width: 85%"
    >
      <div
        v-for="number in numbersList"
        :key="number"
        class="d-flex justify-content-center"
        style="width: 10%"
      >
        <button
          :id="`${number}-btn`"
          class="btn btn-outline-primary m-2"
          style="width: -webkit-fill-available"
          @click="guessNumber(number)"
        >
          <div :id="`${number}-text`" style="visibility: hidden">
            {{ number }}
          </div>
        </button>
      </div>
    </div>
  </div>
</template>
