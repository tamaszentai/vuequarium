<template>
  <div class="fish-tank" ref="fishTank">
    <Fish v-for="fish in props.fishTankFish" :key="fish.id" :name="fish.name" :type="fish.type" :start-x="fish.startX"
          :start-y="fish.startY" :id=fish.id @remove-fish="removeFish"/>
  </div>
</template>

<script setup lang="ts">
import Fish from "@/components/Fish.vue";

interface FishData {
  name: string,
  type: string,
  startX: number,
  startY: number,
  id: string,
}

const props = defineProps({
  fishTankFish: {
    type: Array as () => FishData[],
    required: true,
  }
});
const emit = defineEmits(['addFish', 'removeFish']);

const addFish = () => {
  emit('addFish');
}

const removeFish = (id: string) => {

  emit('removeFish', id);
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