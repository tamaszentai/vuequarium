<script setup lang="ts">

import {computed, ref} from "vue";

const y = ref(0);
const x = ref(0);
const modifiedY = ref(1)
const modifiedX = ref(1)
const isY = ref(true);
const isX = ref(true);

const swim = () => {

  if (y.value >= 550) {
    isY.value = false
  }

  if (y.value <= 0) {
    isY.value = true;
  }

  if (isY.value) {
    y.value += 1;
  }

  if (!isY.value) {
    y.value -= 1;
  }

  if (x.value >= 850) {
    isX.value = false
  }

  if (x.value <= 0) {
    isX.value = true;
  }

  if (isX.value) {
    x.value += 1;
  }

  if (!isX.value) {
    x.value -= 1;
  }
}

const fishCoordinates = computed(() => {
  return {
    transform: `translate(${x.value}px, ${y.value}px)`
  };
});

setInterval(swim, 50);

</script>

<template>
<div class="fish" :style="fishCoordinates">
  <img src="../assets/bluefish.png" alt="fish" />
  <div class="hunger-bar"></div>
</div>
</template>

<style scoped>
.fish {
  width: 150px;
}

.fish img {
  width: 100%;
}

.fish .hunger-bar {
  margin-left: 10%;
  width: 80%;
  height: 10px;
  background-color: salmon;
  border-radius: 50px;
}
</style>