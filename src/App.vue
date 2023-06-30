<template>
  <header>VUEquarium</header>
<main>
  <FishTank />
  <FishSelector />
</main>
</template>

<script setup lang="ts">
import FishTank from "@/components/FishTank.vue";
import FishSelector from "@/components/FishSelector.vue";
</script>



<style scoped>
main {
  display: flex;
}
</style>
