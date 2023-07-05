<script setup lang='ts'>
import { RouterLink } from 'vue-router';


</script>
<template>
   <main>
      <div class="text">
         <h1> Tic-Tac-Toe </h1>
         <h2> Click to start! </h2>
      </div>
      <RouterLink class="btn" to="/game"> Start </RouterLink>
   </main>
</template>
<style scoped>
   @import '../assets/base.css';
   main{
      width: 100%;
      height: 100vh;

      display: flex;
      flex-direction: column;
      justify-content: space-evenly;
      align-items: center;
   }
   .text{
      display: flex;
      flex-direction: column;
      gap: 1rem;
   }
   h1{
      font-size: 4em;
      font-weight: 400;
      letter-spacing: 2px;
      color: rgb(88, 137, 70);
   }
   h2{
      position: relative;

      font-size: 2em;
      font-weight: 400;
      text-align: center;
      letter-spacing: 2px;

      color: rgba(88, 137, 70, 0.534);
   }

   .btn{
      padding: 0.4rem 2rem;

      border: 0.1rem solid rgb(88, 137, 70);
      border-radius: 0.4rem;

      font-size: 1.68em;
      letter-spacing: 1.4px;
      color: rgb(88, 137, 70);

      transition: 0.4s;

      cursor: pointer;
   }
   .btn:hover{
      background-color: rgb(88, 137, 70);
      color: var(--color-background);
   }
</style>
