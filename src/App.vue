<template>
  <div v-if="gameOver==false" id="main" class="main" >
    <div id="header" class="header">TIC-TAC-TOE</div>
    <div id="spacer" class="spacer" />
    <div id="container" class="container">
      <div id="0" class="box"></div>
      <div id="1" class="box"></div>
      <div id="2" class="box"></div>
      <div id="3" class="box"></div>
      <div id="4" class="box"></div>
      <div id="5" class="box"></div>
      <div id="6" class="box"></div>
      <div id="7" class="box"></div>
      <div id="8" class="box"></div>
    </div>
    <button id="reset" class="reset" @click=onClickReset>RESET</button>
  </div>  
  <div v-else id="afterGame" class="afterGame">
    <div id="winner" class="winner">
      PLAYER "{{ winner }}" WON !
    </div>
    <button id="playAgain" class="playAgain" @click=onClickReset>PLAY AGAIN</button>
    <button id="exit" class="exit" @click=onClickExit>EXIT</button>
  </div>
</template>

<style>
.winner{
  font-size:50px;
  font-weight: 700;
  padding:10px 25px;
  margin:10px auto;
}
.afterGame{
  display: flex;
  flex-direction: column;
  width: w-full;
  background-color: grey;
  border-radius: 10px;

}
.main{
  display: flex;
  flex-direction: column;
  width: w-full;
  background-color: grey;
  border-radius: 10px;
}
.header{
  margin:0px 10px;
  font-size: 80px;
  text-align: center;
  color: black;
}
.spacer{
  height: 50px;
}
.container{
  display: grid;
  grid-template-columns: repeat(3, auto);
  width: 306px;
  margin: 40px auto ;
}
.box{
  width: 102px;
  height: 100px;
  padding-bottom: 10px;
  border-radius: 8px;
  border: 2px solid rgb(75, 75, 75);
  cursor: pointer;
  background-color:black;
  line-height: 90px;
  font-size: 90px;
  text-align: center;
  align-content: center;
  color:rgb(75, 75, 75) ;
}
.box:hover{
  background-color:rgb(65, 65, 65); ;
}
.box[clicked]{
  cursor:default;
}
button{
  cursor:pointer;
  font-size:large;
  font-weight: 700;
  background-color: transparent;
  padding:10px 25px;
  margin:10px auto;
  border-radius: 8px;
  border-width: 3px;
}
.reset{
  margin: 50px auto;
}
button:hover{
  background-color:rgb(65, 65, 65);
  color:rgb(176, 176, 176);
}
</style>

<script setup>
import { ref } from 'vue';

let count = 0;
let innerCounterX = 0;
let innerCounterO = 0;
let winner = ref("none");
let gameOver = ref(false);
const arrayX = [];
const arrayO = [];
const winArray = [
  ['0','1','2'],
  ['3','4','5'],
  ['6','7','8'],
  ['0','4','8'],
  ['0','3','6'],
  ['1','4','7'],
  ['2','5','8'],
  ['2','4','6'],
];

const onClickReset = function(){
  location.reload();
}

const onClickExit = function(){
  window.close();
}

const checkerO = function(arrayO,i){
  innerCounterO = 0;
  for (let j = 0; j < arrayO.length; j++) {
    if( winArray[i].includes( arrayO[j] ) ){
      innerCounterO += 1;
      if(innerCounterO == 3){
        return innerCounterO;
      }
    } 
  }
  
}

const checkerX = function(arrayX,i){
  innerCounterX = 0;
  for (let j = 0; j < arrayX.length; j++) {
    if( winArray[i].includes( arrayX[j] ) ){
      innerCounterX += 1;
      if(innerCounterX == 3){
        return innerCounterX;
      }
    } 
  }
}

const findWinner1 = function(arrayX ,arrayO){
  for (let i = 0; i < winArray.length; i++) {
    innerCounterO = checkerO(arrayO,i);
    innerCounterX = checkerX(arrayX,i);
    if( innerCounterX==3 ){
      winner.value = "X";
      break;
    }else if( innerCounterO==3 ){
      winner.value = "O";
      break;
    }
  }
  if(winner.value != "none"){
    gameOver.value = true;
  }
}

const returnSymbol = function(){
  if (count % 2 == 0) {
    return "X";
  } else{
    return "O";
  }
}

const checkGame = function(ele,sym){
  if (sym === 'X'){
    arrayX.push(ele);
  }else{
    arrayO.push(ele);
  }
  if ((arrayX.length >= 3) || (arrayO.length >= 3)){
    findWinner1(arrayX,arrayO)
  }
}

const onClickBox = (event) => {
  const element = document.getElementById(event.srcElement.id)
  if (element.className === "box"){
    if(element.hasAttribute("clicked")){
      return;
    }
    count +=1;
    element.setAttribute("clicked" , "true");
    const symbol = returnSymbol();
    element.innerHTML = symbol;
    checkGame(element.id,symbol);
  }
  if(count == 9){
    location.reload();
  }
}
document.addEventListener('click', onClickBox);
</script>
