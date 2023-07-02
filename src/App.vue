<template>
  <header><h1 class="font-effect-shadow-multiple">VUEquarium</h1></header>
<main>
  <FishTank :fish-tank-fish="fishTankFish" @remove-fish="removeFish"/>
  <FishSelector @add-fish="addFish"/>
</main>
</template>

<script setup lang="ts">
import FishTank from "@/components/FishTank.vue";
import FishSelector from "@/components/FishSelector.vue";
import {ref} from "vue";

interface FishData {
  name: string,
  type: string,
  startX: number,
  startY: number,
  id: string,
}

const fishTankFish = ref<FishData[]>([]);

const addFish = (payload) => {
  // fishTankFish.value.push({name: 'Joe', type: 'golden', startX: 600, startY: 50},
  //     {name: 'Bob', type: 'blue', startX: 100, startY: 500},
  //     {name: 'Dessia', type: 'ray', startX: 200, startY: 100},
  //     {name: 'Wayne', type: 'puffer', startX: 300, startY: 200},
  //     {name: 'Alice', type: 'sword', startX: 400, startY: 300},
  // );

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
  font-family: "Rancho", serif ;
}
main {
  display: flex;
  justify-content: center;
}
</style>
