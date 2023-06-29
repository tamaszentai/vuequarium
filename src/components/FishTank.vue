<template>
  <div class="fish-tank" ref="fishTank">
    <Fish v-for="fish in fishTankFish" :key="fish.name" :name="fish.name" :type="fish.type" :start-x="fish.startX"
          :start-y="fish.startY" />
    <button @click="addFish">add fish</button>
  </div>
</template>

<script setup lang="ts">
import Fish from "@/components/Fish.vue";
import { ref } from "vue";

interface FishData {
  name: string,
  type: string,
  startX: number,
  startY: number,
}

const fishTankFish = ref<FishData[]>([]);

const addFish = () => {
  fishTankFish.value.push({name: 'Joe', type: 'golden', startX: 600, startY: 50},
      {name: 'Bob', type: 'blue', startX: 100, startY: 500},
      {name: 'Dessia', type: 'ray', startX: 200, startY: 100},
      {name: 'Wayne', type: 'puffer', startX: 300, startY: 200}
  )
}

</script>

<style scoped>
.fish-tank {
  width: 1024px;
  height: 680px;
  background-image: url("../assets/fish-tank.png");
  background-size: 100%;
  background-repeat: no-repeat;
  border: 20px solid goldenrod;
}
</style>