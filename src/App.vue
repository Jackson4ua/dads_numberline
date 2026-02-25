<script setup lang="ts">
const numbersList: Ref<number[]> = []

for (let i = 1; i <= 100; i++) {
  numbersList.push(i)
}

function revealNumber(number: any) {
  document
    .getElementById(`${number}-btn`)!
    .style
    .setProperty('visibility', 'visible')
  setTimeout(() => {
    document
      .getElementById(`${number}-btn`)!
      .style
      .setProperty('visibility', 'hidden')
  }, 1500)
}
</script>

<template>
  <div class="d-flex flex-column justify-content-center align-items-center">
    <div class="m-1">
      <h2 class="display-2">
        Mr. Holbrook's Number Line
      </h2>
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
          class="btn btn-outline-primary m-2"
          style="width: -webkit-fill-available"
          @click="revealNumber(number)"
        >
          <div :id="`${number}-btn`" style="visibility: hidden">
            {{ number }}
          </div>
        </button>
      </div>
    </div>
  </div>
</template>
