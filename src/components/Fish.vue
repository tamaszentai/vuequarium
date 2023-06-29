<template>
  <div class="fish" :style="fishCoordinates">
    <div class="name">{{props.name}}</div>
    <img :src="`/src/assets/${fishType}`" :alt="`${fishType}`" :style="flipFish" />
    <div class="hunger-bar"></div>
  </div>
</template>

<script setup lang="ts">
import {computed, ref} from "vue";

const y = ref(props.startY);
const x = ref(props.startX);
const modifiedY = ref(1)
const modifiedX = ref(1)
const isY = ref(true);
const isX = ref(true);

const props = defineProps<{
  name: string
  type: string
  startX: number
  startY: number
}>();

const generateRandomNumber = () => {
  const numbers = [35, 45, 55, 65];
  const randomIndex = Math.floor(Math.random() * numbers.length);
  return numbers[randomIndex];
}

let randomSpeed = generateRandomNumber();

const fishType = computed(() => {
  let image = '';
  switch(props.type) {
    case 'golden':
      image = 'goldfish.png';
      break;
    case 'blue':
      image = 'bluefish.png';
      break;
    case 'ray':
      image = 'mantaray.png';
      break;
    case 'puffer':
      image =  'pufferfish.png';
      break;
  }
  return image;
})

const swim = () => {

  if (y.value >= 500) {
    isY.value = false
    randomSpeed = generateRandomNumber();
    console.log(randomSpeed);
  }

  if (y.value <= 0) {
    isY.value = true;
    randomSpeed = generateRandomNumber();
  }

  if (isY.value) {
    y.value += 1;
  }

  if (!isY.value) {
    y.value -= 1;
  }

  if (x.value >= 850) {
    isX.value = false
    randomSpeed = generateRandomNumber();
  }

  if (x.value <= 0) {
    isX.value = true;
    randomSpeed = generateRandomNumber();
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
    transform: `translate(${x.value}px, ${y.value}px`
  };
});

const flipFish = computed(() => {
  return {
    transform: `${isX.value ? "" : " scaleX(-1)"}`, transition: 'transform 0.5s'
  }
})

setInterval(swim, randomSpeed);

</script>

<style scoped>
.fish {
  width: 150px;
  position: absolute;
  //border: 3px solid black;
}

.name {
  background-color: rgba(219,203,187, 0.8);
  text-align: center;
  font-size: 1.5rem;
  border-radius: 50px;
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