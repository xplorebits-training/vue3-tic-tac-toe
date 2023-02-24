<template>
  <div id="main" class="main" >
    <div id="header" class="header">TIC-TAC-TOE</div>
    <div id="spacer" class="spacer" />
    <div id="container" class="container">
      <div id="box0" class="box"></div>
      <div id="box1" class="box"></div>
      <div id="box2" class="box"></div>
      <div id="box3" class="box"></div>
      <div id="box4" class="box"></div>
      <div id="box5" class="box"></div>
      <div id="box6" class="box"></div>
      <div id="box7" class="box"></div>
      <div id="box8" class="box"></div>
    </div>
    <button id="reset" class="reset" @click=onClickReset>RESET</button>
  </div>
</template>

<style>
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
.reset{
  cursor:pointer;
  font-size:large;
  font-weight: 700;
  background-color: transparent;
  padding:10px 25px;
  margin: 50px auto;
  border-radius: 8px;
  border-width: 3px;
}
.reset:hover{
  background-color:rgb(65, 65, 65);
  color:rgb(176, 176, 176);
}
</style>

<script setup>
let count = 0;

const returnSymbol = function(){
  if (count % 2 == 0) {
    return "X";
  } else{
    return "O";
  }
}

const onClickReset = function(){
  location.reload()
}

const onClickBox = (event) => {
  const element =  document.getElementById(event.srcElement.id)
  if (element.className === "box"){
    if(element.hasAttribute("clicked")){
      return;
    }
    count +=1;
    element.setAttribute("clicked" , "true");
    const symbol = returnSymbol();
    element.innerHTML = symbol;
  }
}
document.addEventListener('click', onClickBox);
</script>
