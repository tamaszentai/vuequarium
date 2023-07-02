<template>
  <div class="fish" :style="fishCoordinates">
    <div class="data-container">
      <div v-if="notification" class="notification">FEED ME!</div>
      <div class="name">{{ props.name }}</div>
    </div>
    <div class="wrapper" :style="startDirection" @click="feedFish">
      <img :src="isDead ? `${skeleton}`: `${fishType}`" :alt="`${fishType}`"
           :style="flipFish">
    </div>
    <div v-if="!isDead" class="stomach">
      <div class="hunger-bar" :style="hungriness"></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import {computed, onMounted, ref} from "vue";
import golden from "@/assets/goldfish.png";
import blue from "@/assets/bluefish.png";
import ray from "@/assets/mantaray.png";
import puffer from "@/assets/pufferfish.png";
import sword from "@/assets/swordfish.png";
import skeleton from "@/assets/fishskeleton.png";

const props = defineProps<{
  name: string
  type: string
  startX: number
  startY: number
  id: string
}>();

const y = ref(props.startY);
const x = ref(props.startX);
const isY = ref(true);
const isX = ref(true);
const directionName = ref('');
const stomach = ref(100);
const isDead = ref(false);


const emit = defineEmits(['remove-fish']);

onMounted(() => {
  leftOrRightFloat();
});

const generateRandomNumber = () => {
  const numbers = [35, 45, 55, 65];
  const randomIndex = Math.floor(Math.random() * numbers.length);
  return numbers[randomIndex];
}

const leftOrRightFloat = () => {
  const direction = ['left', 'right'];
  const random = Math.floor(Math.random() * 2);
  directionName.value = direction[random];
  return direction[random];
}

let randomSpeed = generateRandomNumber();

const fishType = computed(() => {
  let image = '';
  switch (props.type) {
    case 'golden':
      image = golden;
      break;
    case 'blue':
      image = blue;
      break;
    case 'ray':
      image = ray;
      break;
    case 'puffer':
      image = puffer;
      break;
    case 'sword':
      image = sword;
      break;
  }
  return image;
})

const swim = () => {
  if (!isDead.value) {
    if (directionName.value === 'right') {
      if (y.value >= 410 || y.value <= 0) {
        isY.value = !isY.value;
        randomSpeed = generateRandomNumber();
      }

      y.value += isY.value ? 1 : -1;

      if (x.value >= 830 || x.value <= 0) {
        isX.value = !isX.value;
        randomSpeed = generateRandomNumber();
      }

      x.value += isX.value ? 1 : -1;
    }


    if (directionName.value === 'left') {
      if (y.value >= 410 || y.value <= 0) {
        isY.value = !isY.value;
        randomSpeed = generateRandomNumber();
      }

      y.value -= isY.value ? 1 : -1;

      if (x.value >= 830 || x.value <= 0) {
        isX.value = !isX.value;
        randomSpeed = generateRandomNumber();
      }
      x.value -= isX.value ? 1 : -1;
    }
  }

  if (isDead.value) {
    y.value += 1;
    if (y.value >= 500) {
      y.value = 500;
      setTimeout(() => {
        emit('remove-fish', props.id);
      }, 10000)
    }
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

const startDirection = computed(() => {
  return {
    transform: `${directionName.value === 'right' ? "" : "scaleX(-1)"}`
  }
})

const hungriness = computed(() => {
  return {
    width: `${stomach.value}%`,
    backgroundColor: `${stomach.value > 50 ? 'green' : stomach.value > 20 ? 'orange' : 'red'}`
  }
})

const notification = computed(() => {
  return stomach.value <= 20 && isDead.value === false
})

const hunger = () => {
  if (stomach.value === -50) {
    isDead.value = true;
    return
  }
  stomach.value -= 1;
}

const feedFish = () => {
  stomach.value = 100;
}

setInterval(swim, randomSpeed);
setInterval(hunger, 200); // 200

</script>

<style scoped>
.fish {
  width: 150px;
  position: absolute;
}

.data-container {
  height: 4rem;
  position: relative;

}

@keyframes changeFontSize {
  0% {
    font-size: 1.5rem;
    color: salmon;
  }
  50% {
    font-size: 2rem;
    color: red;
  }
  100% {
    font-size: 1.5rem;
    color: salmon;
  }
}

.notification {
  text-align: center;
  animation-name: changeFontSize;
  animation-duration: 2s;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}

.name {
  background-color: rgba(219, 203, 187, 0.8);
  text-align: center;
  font-size: 1.5rem;
  position: absolute;
  top: 75%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.fish img {
  width: 100%;
}

.fish img:hover {
  cursor: pointer;
}

.stomach {
  margin-left: 10%;
  width: 80%;
  height: 10px;
  background-color: white;
  border-radius: 50px;
}

.hunger-bar {
  height: 100%;
  border-radius: 50px;
}
</style>