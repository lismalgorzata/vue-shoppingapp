<template>
  <div>
    <app-headers />
    <Container />
  </div>
</template>

<script setup>

import AppHeaders from './components/AppHeaders.vue';
import Container from './components/Container.vue';

</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Inter&family=Rajdhani:wght@500&display=swap');

body{
  font-family: 'Rajdhani', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: rgb(220, 202, 220);
}
</style>
