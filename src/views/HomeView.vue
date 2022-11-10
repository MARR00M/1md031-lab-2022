<template> 
<header>
      <img src="IMG_6544.JPG" id="TopPic" title="TopPic">
      <h1 id="Title">Välkommen Till De Vänner Du Behöver</h1>
    </header>

    <h2><nav> Välj din vän</nav></h2>

   <main>
        <section>
         <div class="wrapper"> 
            <div class="menuitem" id="MysIsak">
            <h3>MysIsak</h3>
            <img src="20211204_004757.jpg" title="MysIsak" style="width: 200px">
            <footer>
               <div class="description">
                  <p>Mysig</p>
                  <p>Rolig</p>
                  Pris: 200SEK
               </div>
             </footer>
            </div><div class="menuitem" id="GrönaFaran">
            <h3>Gröna Faran</h3>
            <img src="20220115_213531.jpg" title="Gröna faran" style="width: 200px">
            <footer>
               <div class="description">
                  <p>Livlig</p>
                  <p>Stark -Vilka Biccar-</p>
                  Pris: 2.000SEK
               </div>
             </footer>
            </div><div class="menuitem" id="FruBillys">
            <h3>FruBillys</h3>
            <img src="20220410_122544.jpg" title="FruBillys" style="width: 200px">
            <footer>
               <div class="description">
                  <p>Har alltid med sig Billys</p>
                  <p>Stylish</p>
                  Pris: 250SEK
               </div>
             </footer>
            </div><div class="menuitem" id="FBFB">
            <h3>FB-FB</h3>
            <img src="20220402_192541.jpg" title="FB-FB" style="width: 200px">
            <footer>
               <div class="description">
               <p>Tar alltid med sig festen</p>
               <p>Försvinner i dimman</p>
               Pris: 0.25SEK
            </div>
             </footer>
            </div><div class="menuitem" id="Cutiee">
            <h3>The Cutiee</h3>
            <img src="20220122_011611.jpg" title="The Cutiee" style="width: 200px">
            <footer>
               <div class="description">
                  <p>Gullig</p>
                  <p>Bästa snusvännen</p>
                  Pris: 2MSEK
               </div>
             </footer>
            </div>
          </div>
         </section>
    

      <section>
         <h2>Kundinformation</h2>
         <div>
            Nedan fyller du i all nödvändig information
            <h3>Nödvändig Information För Att Skapa Er Vänskap</h3>
            <h4>Ditt Fullständiga Namn</h4>
            <input type="text" placeholder="För- och Efternamn">
            <h4>Din E-mail</h4>
            <input type="text" placeholder="E-mail">
            <h4>Dubbellkolla att allt ovan stämmer inann du beställer</h4>
            <button> Beställ </button>
         </div>
      </section>
   </main>

<div>
   <footer>
      <h2><nav> Kontaktinformation </nav></h2>
      För kontakt ring 018-vi-finns-här-för-dig
   </footer>
</div>
  <div>
    <div>
      {{namn}}
      Friends
      <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"/>
    </div>
    Namn: <input type="text" v-model="namn" placeholder="För- och Efternamn">
    <div id="map" v-on:click="addOrder">
      click here
    </div>
  </div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

let friends =[
  {name: "MysIsak", price: 200, URL: "20211204_004757.jpg", atributes: ["Mysig", "Rolig"]},
  {name: "GrönaFaran", price: 250, URL: "20220115_213531.jpg", atributes: ["Livlig", "Stark -kolla in biccarna-"]},
  {name: "FruBillys", price: 275, URL: "20220410_122544.jpg", atributes: ["Har alltid med sig Billys", "Stylish"]},
  {name: "FB-FB", price: 0.25, URL: "20220402_192541.jpg", atributes: ["Tar alltid med sig festen", "Försvinner i dimman"]},
  {name: "TheCutiee", price: 2000, URL: "20220122_011611.jpg", atributes: ["Gullig", "Bästa snusvännen"]},
]

function MenuItem(name, URL, price, atributes){

}

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: friends, 
      namn: "",
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.offsetX - 10, //generalisera hårdkodningen (10 är inge bra, gör den relativ till cirkelns radie)
                                           y: event.offsetY - 10},
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';

header{
   position: relative;
   text-align: center;
   margin: 2%;
   overflow: hidden;
 }

 #TopPic{
   opacity: 0.75;
   width: 96vw; 
   height: 40vh;
 }

 #Title{
   position: relative;
   top: -20vh;
   color: white;
 }

body {
    font-family: Cambria;
    color: rgb(15, 15, 15);
    font-size: larger;
 }
 section{
   border: dashed;
   margin: 2%;
}
 div {
    margin: 2%;
 }

h2 {
   margin: 2%;
 }

 .description p {
    font-weight: bold;
 }

 button:hover {
   background-color: #8cd8b9;
   cursor: pointer;
}

.wrapper {
   display: flex;
}

.menuitem{
   flex-grow: 1;
   margin: 0%;
   text-align: center;
 }

 #MysIsak{
    background-color: #8cd8b9;
    color: rgb(0, 0, 0);
    grid-column: 1;
    grid-row: 1;
 }

 #GrönaFaran{
    background-color: #56c699;
    color: rgb(0, 0, 0);
    grid-column: 2;
    grid-row: 1;
 }

 #FruBillys{
    background-color: #35a075;
    color: rgb(255, 255, 255);
    grid-column: 3;
    grid-row: 1;
}

#FBFB{
    background-color: #236a4e;
    color: rgb(255, 255, 255);
    grid-column: 4;
    grid-row: 1;
}

#Cutiee{
    background-color: #1a503a;
    color: rgb(255, 255, 255);
    grid-column: 5;
    grid-row: 1;
}

  #map {
    width: 300px;
    height: 300px;
    background-color: red;
    cursor: pointer;
  }
  #map:hover {
    background-color: pink;
  }
  input {
    font-family: Cambria;
  }
</style>