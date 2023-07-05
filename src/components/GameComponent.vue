<script setup lang='ts'>
   import { ref, onMounted } from "vue"

   const resultPage = ref()
   const resultText = ref<string>()

   const cells = ref<Element[]>([])

   const board = ref<string[]>([])
   const player = ref<string>("X")

   const isGameActive = ref<boolean>()

   const winCombos = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
  ];

   function startGame(){
      createBoard()
      resultPage.value.classList.add("hide")
      isGameActive.value = true
   }

   function createBoard(){
      board.value = ["","","","","","","","",""]
      player.value = "X"
   }

   function changeCell(index: number){
      if(isGameActive.value){
         if(board.value[index] === ""){
            board.value[index] = player.value

            cells.value[index].classList.add(`cell-${player.value}`)
            
            if(!checkWin()){
               playerSide()
            }
         }
      }
   }

   function playerSide(){
      if(player.value === "X"){
         player.value = "O"
      }
      else{
         player.value = "X"
      }
   }

   function checkWin(){
      let isDraw = true
      let win = false

      winCombos.forEach(e => {
         if(board.value[e[0]] === player.value && board.value[e[1]] === player.value && board.value[e[2]] === player.value){
            win = true
         }
      })

      if(win){
         result(`Player - "${player.value}" win!`)
         isGameActive.value = false

         return true
      }

      board.value.forEach(e => {
         if(isDraw){
            if(e === ""){
               isDraw = false
            }
         }
      })

      if(isDraw){
         result(`Draw!`)
         isGameActive.value = false

         //window.open("https://sun1-29.userapi.com/impg/_Sweg_diEqj7tRd4nA2s5rVq6HbVJQdns88Wbg/hSgaxOJrKJo.jpg?size=944x1080&quality=95&sign=e84fd81f76754ffc58a93d8af1ee407a&type=album", "blank", "width=1920,height=1080")
         return true
      }

      return false
   }

   function result(text: string){
      resultPage.value.classList.remove("hide")
      resultText.value = text
   }

   onMounted(() => {
      startGame()
   })
</script>
<template>
   <main>
      <div class="resultPage" ref="resultPage">
         <h1> {{ resultText }} </h1>
      </div>

      <div class="board">
         <h1 class="cell" v-for="(cell, index) in board"  @click="changeCell(index)" ref="cells"> {{ cell }}</h1>
      </div>

      <div class="controllers">
         <div class="btn" @click="startGame"> restart </div>
      </div>
   </main>
</template>
<style scoped>
   main{
      position: relative;

      width: 100%;
      height: 100vh;

      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
   }
   .resultPage{
      position: absolute;
      top: 0;
      right: 0;
      
      padding: 0.4rem;

      width: 100%;

      display: flex;
      justify-content: center;
      align-items: center;

      color: var(--color-background);
      background-color: rgb(88, 137, 70);

      transform: translateY(0rem);
      transition: 0.6s;
   }
   .board{
      width: auto;
      height: auto;

      display: grid;
      grid-template-columns: repeat(3,1fr);
   }
   .cell{
      width: 120px;
      height: 120px;

      display: flex;
      justify-content: center;
      align-items: center;

      font-size: 4rem;
      text-align: center;

      cursor: pointer;
      transition: 0.4s;
      opacity: 1;
   }

   .cell:nth-child(2){
      border-left: 0.2rem solid rgb(88, 137, 70);
      border-right: 0.2rem solid rgb(88, 137, 70);
   }

   .cell:nth-child(4){
      border-top: 0.2rem solid rgb(88, 137, 70);
      border-bottom: 0.2rem solid rgb(88, 137, 70);
   }
   .cell:nth-child(5){
      border: 0.2rem solid rgb(88, 137, 70);
   }
   .cell:nth-child(6){
      border-top: 0.2rem solid rgb(88, 137, 70);
      border-bottom: 0.2rem solid rgb(88, 137, 70);
   }

   .cell:nth-child(8){
      border-left: 0.2rem solid rgb(88, 137, 70);
      border-right: 0.2rem solid rgb(88, 137, 70);
   }
   .hide{
      transform: translateY(-10rem);
   }

   .controllers{
      padding-top: 2rem;
   }
   .btn{
      padding: 0.4rem 2rem;

      border: 0.1rem solid rgb(88, 137, 70);
      border-radius: 0.4rem;

      font-size: 1.68em;
      letter-spacing: 1.4px;
      
      background-color: rgb(88, 137, 70);
      color: var(--color-background);

      transition: 0.4s;

      cursor: pointer;
   }
   .btn:hover{
      background-color: var(--color-background);
      color: rgb(88, 137, 70);
   }
</style>
