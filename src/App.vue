<script setup>
import MAPS from 'svg-maps';
import Map from './Map.vue';
console.log(MAPS.USA);
</script>

<template>
  <Map
    :map="MAPS.USA"
    location-role="link"
	/>
</template>

<style scoped>

</style>
