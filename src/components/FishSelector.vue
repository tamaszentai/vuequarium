<template>
  <div class="fish-selector">
    <h1>Choose a fish:</h1>
    <div class="fish-list">
      <ul>
        <li v-for="fish in fishList" :key="fish.type" @click="selectFish(fish.type)"
            :class="fish.isSelected ? 'selected' : ''">
          <img :src="fish.isSelected ? fish.selectedImage :fish.image" :alt="fish.type"/>
        </li>
      </ul>
    </div>
    <input type="text" placeholder="Enter a name for your fish" v-model="fishName"/>
    <br/>
    <button @click="addFish">ADD FISH</button>
  </div>

</template>

<script setup lang="ts">
import golden from "@/assets/goldfish.png";
import goldenSelected from "@/assets/goldfish-glow.png";
import blue from "@/assets/bluefish.png";
import blueSelected from "@/assets/bluefish-glow.png";
import ray from "@/assets/mantaray.png";
import raySelected from "@/assets/mantaray-glow.png";
import puffer from "@/assets/pufferfish.png";
import pufferSelected from "@/assets/pufferfish-glow.png";
import sword from "@/assets/swordfish.png";
import swordSelected from "@/assets/swordfish-glow.png";
import {ref} from "vue";


const emit = defineEmits(['addFish']);

const fishList = ref([
  {type: 'golden', image: golden, selectedImage: goldenSelected, isSelected: false},
  {type: 'blue', image: blue, selectedImage: blueSelected, isSelected: false},
  {type: 'ray', image: ray, selectedImage: raySelected, isSelected: false},
  {type: 'puffer', image: puffer, selectedImage: pufferSelected, isSelected: false},
  {type: 'sword', image: sword, selectedImage: swordSelected, isSelected: false},
]);

const fishName = ref('');

const selectFish = (type: string) => {
  fishList.value.forEach(fish => {
    fish.isSelected = fish.type === type;
  });
}

const randomX = () => {
  return Math.floor(Math.random() * 800);
}

const randomY = () => {
  return Math.floor(Math.random() * 400);
}

const addFish = () => {
  const selectedFish = fishList.value.find(fish => fish.isSelected);
  if (!selectedFish || !fishName.value) {
    return;
  }
  const payload = {
    type: selectedFish.type,
    name: fishName.value,
    startX: randomX(),
    startY: randomY(),
  }

  fishList.value.forEach(fish => {
    fish.isSelected = false;
  });

  fishName.value = '';

  console.log(payload);
  emit('addFish', payload);
}

</script>


<style scoped>
.fish-selector {
  text-align: center;
  height: 680px;
  width: 500px;
  border: 20px solid goldenrod;
  background-color: bisque;
}

h1 {
  font-family: "Rancho", serif;
  font-size: 3rem;
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
  margin: 5px;
}

li:hover {
  cursor: pointer;
}


img {
  width: 100px;
  margin: 1rem;
}

input[type=text] {
  width: 80%;
  margin: 0 0 1rem 0;
  padding: 1rem;
  font-size: 1.5rem;
  background-color: whitesmoke;
  border-radius: 20px;
  font-family: "Times New Roman", serif;
}

button {
  height: 3rem;
  width: 6rem;
  border-radius: 50px;
  background-color: lightblue;
  font-weight: bold;
  font-size: 1rem;
  font-family: "Rancho", serif;
}
</style>