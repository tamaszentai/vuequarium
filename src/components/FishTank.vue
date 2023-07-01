<template>
  <div class="fish-tank" ref="fishTank">
    <Fish v-for="fish in props.fishTankFish" :key="fish.name" :name="fish.name" :type="fish.type" :start-x="fish.startX"
          :start-y="fish.startY" />
  </div>
</template>

<script setup lang="ts">
import Fish from "@/components/Fish.vue";
import {defineEmits} from "vue";

const props = defineProps({
  fishTankFish: {
    type: Array,
    required: true,
  }
});
const emit = defineEmits(['addFish']);

const addFish = () => {
  emit('addFish');
}

</script>

<style scoped>
.fish-tank {
  display: inline-block;
  width: 1024px;
  height: 680px;
  background-image: url("../assets/fish-tank.png");
  background-size: 100%;
  background-repeat: no-repeat;
  border: 20px solid goldenrod;
}
</style>