<template>
  <header>VUEquarium</header>
<main>
  <FishTank :fish-tank-fish="fishTankFish"/>
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
</script>



<style scoped>
main {
  display: flex;
}
</style>
