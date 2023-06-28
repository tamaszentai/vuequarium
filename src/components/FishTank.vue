<script setup lang="ts">

import Fish from "@/components/Fish.vue";
</script>

<template>
<div class="fish-tank">
  <Fish />
</div>
</template>

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