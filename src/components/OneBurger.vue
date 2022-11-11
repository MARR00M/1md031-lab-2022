<template>
            <div class="menuitem">
            <h3>{{ burger.name }}</h3>
            <img class="image" v-bind:src="burger.imgSrc">
            <footer>
               <div class="description">
                  <p>{{ burger.atributes[0] }}</p>
                  <p>{{ burger.atributes[1] }}</p>
                  Pris: {{ burger.price }}SEK
               </div>
             </footer>
             </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
 div {
    margin: 2%;
 }

.menuitem{
   flex-grow: 1;
   margin: 0%;
   text-align: center;
   background-color: #8cd8b9;
   color: rgb(0, 0, 0);
 }

 .image{
  width: 12vw;
  height: 16vw;
 }
 
 .description p {
    font-weight: bold;
 }
  </style>
  