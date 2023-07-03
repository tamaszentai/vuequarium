<template>
  <div v-if="isAboveResolution">
  <header><h1 class="font-effect-shadow-multiple">VUEquarium</h1></header>
  <main>
    <FishTank :fish-tank-fish="fishTankFish" @remove-fish="removeFish"/>
    <FishSelector @add-fish="addFish"/>
  </main>
  </div>
  <div v-else class="warning">
    <h1>For the optimal experience make sure your resolution is equal to or higher than 1520x860</h1>
    <button @click="reloadPage">Everything is fine now, reload!
    </button>
  </div>
</template>

<script setup lang="ts">
import FishTank from "@/components/FishTank.vue";
import FishSelector from "@/components/FishSelector.vue";
import {onMounted, ref, watch} from "vue";

interface FishData {
  name: string,
  type: string,
  startX: number,
  startY: number,
  id: string,
}

const minWidth = 1520;
const minHeight = 860;
const fishTankFish = ref<FishData[]>([]);
const isAboveResolution = ref(false);

const reloadPage = () => {
  location.reload();
};

onMounted(() => {
  isAboveResolution.value =
      window.innerWidth >= minWidth && window.innerHeight >= minHeight;
});



const addFish = (payload: FishData) => {
  fishTankFish.value.push(payload);
}

const removeFish = (id: string) => {
  const index = fishTankFish.value.findIndex(fish => fish.id === id);
  fishTankFish.value.splice(index, 1);
}
</script>


<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-user-select: none; /* Safari */
  -ms-user-select: none; /* IE 10 and IE 11 */
  user-select: none; /* Standard syntax */
}

html, body {
  background-color: lightgreen;
}

</style>

<style scoped>


header {
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  color: black;
  margin: 3rem 0;
  font-family: "Rancho", serif;
}

main {
  display: flex;
  justify-content: center;
}

.warning {
  margin-top: 10rem;
  padding: 0 2rem;
  text-align: center;
  font-family: "Rancho", serif;
}

button {
  height: auto;
  width: auto;
  margin-top: 2rem;
  padding: 0 1rem;
  border-radius: 50px;
  background-color: lightblue;
  font-size: 2rem;
  font-family: "Rancho", serif;

}
</style>
