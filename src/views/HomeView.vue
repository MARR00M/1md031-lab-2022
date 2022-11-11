<template> 

<div>
  <header>
      <img src="IMG_6544.JPG" id="TopPic" title="TopPic">
      <h1 id="Title">Välkommen Till De Vänner Du Behöver</h1>
    </header>
   <main>
      <h2>Vänner på lager</h2>
      <section>
        <div class="wrapper">
      <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"/>
            </div>
            </section>
      <section>
         <h2>Beställningsinformation</h2>
         <div>
            <h3>Nödvändig Information För Att Skapa Er Vänskap</h3>
            <h4>Ditt Fullständiga Namn</h4>
            <input type="text" v-model="namn" placeholder="För- och Efternamn">{{namn}}
            <h4>Din E-mail</h4>
            <input type="text" v-model="eMail" placeholder="E-mail">{{eMail}}
            <h4>Vart du vill mötas upp</h4>
            <div id="map" v-on:click="addOrder">
            click here
            </div>
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
  </div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

let friends =[
  {name: "MysIsak", price: 200, imgSrc: "20211204_004757.jpg", atributes: ["Mysig", "Rolig"],  column: 1, row: 1},
  {name: "GrönaFaran", price: 250, imgSrc: "20220115_213531.jpg", atributes: ["Livlig", "Stark -kolla in biccarna-"],  column: 2, row: 1},
  {name: "FruBillys", price: 275, imgSrc: "20220410_122544.jpg", atributes: ["Har alltid med sig Billys", "Stylish"],  column: 3, row: 1},
  {name: "FB-FB", price: 0.25, imgSrcL: "20220402_192541.jpg", atributes: ["Tar alltid med sig festen", "Försvinner i dimman"],  column: 4, row: 1},
  {name: "TheCutiee", price: 2000, imgSrc: "20220122_011611.jpg", atributes: ["Gullig", "Bästa snusvännen"],  column: 5, row: 1},
]

function MenuItem(name, imgSrc, price, atributes){

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
   margin: -2%;
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

 button:hover {
   background-color: #8cd8b9;
   cursor: pointer;
}

.wrapper {
   display: flex;
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