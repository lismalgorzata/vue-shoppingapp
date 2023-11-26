<template>
  <div class="appHeader">
    <div class="logo">Bonita</div>
    <div>Fashion on your terms - shop online with style!</div>
    <div @click="goToMainPage" class="homeIcon">
      <svg 
        xmlns="http://www.w3.org/2000/svg" 
        width="24" 
        height="24" 
        viewBox="0 0 24 24" 
        fill="none" 
        stroke="currentColor" 
        stroke-width="2" 
        stroke-linecap="round" 
        stroke-linejoin="round" 
        class="feather feather-home">
        
        <path 
        d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/>
        <polyline points="9 22 9 12 15 12 15 22"/>
      </svg>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const goToMainPage = () => {
  router.push({ name: 'home' });
};
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Ephesis&family=Rajdhani:wght@500&family=Satisfy&display=swap');

.appHeader{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 48px;
    border-bottom: 1px solid grey;
    background-color: rgb(190, 161, 190);
    font-family: 'Satisfy', cursive;
    font-size: xx-large;
}
.logo{
    cursor: pointer;
    font-weight: 600;
    font-size: 20px;
    letter-spacing: 12px;
    font-family: 'Ephesis', cursive;
    font-size: x-large;
    color: rgb(125, 42, 153);
}
.homeIcon{
  cursor: pointer;
  color: rgb(125, 42, 153)
}
.homeIcon:hover{
  color: rgb(134, 93, 172);
}
</style>
