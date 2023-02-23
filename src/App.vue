<template>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@0.7.4/dist/tailwind.min.css" rel="stylesheet">

  <div class="w-full h-10 bg-red">may be works</div>
  <div class="flex flex-col w-full bg-grey" >
      <div class=" text-2xl text-center text-black">TIC-TAC-TOE</div>
      <div class="h-24" />
      <div class="container">
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
        <div class="box"></div>
      </div>
  </div>
</template>
<style>
.container{
  display: grid;
  grid-template-columns: repeat(3, auto);
  width: 306px;
  margin: 10px auto;
}
.box{
  width: 100px;
  height: 100px;
  border: 2px solid #ffffff;
  cursor: pointer;
  background-color:grey;
  line-height: 100px;
  font-size: 60px;
}
</style>