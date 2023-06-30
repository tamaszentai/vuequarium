<template>
  <div class="fish-selector">
    <h1>Choose a fish</h1>
    <div class="fish-list">
      <ul>
        <li v-for="fish in fishList" :key="fish.type" @click="selectFish(fish.type)" :class="fish.isSelected ? 'selected' : ''">
          <img :src="fish.image" :alt="fish.type" />
        </li>
      </ul>
    </div>
    <input type="text" placeholder="Enter a name for this fish" v-model="fishName"/>
    <br />
    <button @click="addFish">Add fish</button>
  </div>

</template>

<script setup lang="ts">
import golden from "@/assets/goldfish.png";
import blue from "@/assets/bluefish.png";
import ray from "@/assets/mantaray.png";
import puffer from "@/assets/pufferfish.png";
import sword from "@/assets/swordfish.png";
import {ref} from "vue";

const fishList = ref([
  {type: 'golden', image: golden, isSelected: false},
  {type: 'blue', image: blue, isSelected: false},
  {type: 'ray', image: ray, isSelected: false},
  {type: 'puffer', image: puffer, isSelected: false},
  {type: 'sword', image: sword, isSelected: false},
]);

const fishName = ref('');

const selectFish = (type: string) => {
  fishList.value.forEach(fish => {
    fish.isSelected = fish.type === type;
  });
}

const addFish = () => {
  const selectedFish = fishList.value.find(fish => fish.isSelected);
  const payload = {
    type: selectedFish.type,
    name: fishName.value,
  }

  console.log(payload);
}

</script>



<style scoped>
 .fish-selector {
   text-align: center;
   margin-left: 3rem;
   height: 680px;
   width: 500px;
   border: 1px solid black;
 }

 h1 {
    font-family: "Comic Sans MS", cursive, sans-serif;
 }

 .fish-list {

   display: flex;

 }

 ul {
    list-style: none;
 }

 li {
   display: inline-block;
    padding: 1rem;
 }

 li:hover {
   cursor: pointer;
   border: 1px solid black;
 }

 .selected {
   border: 1px solid black;
 }

 img {
   width: 100px;
   margin: 1rem;
 }
</style>