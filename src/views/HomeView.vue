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
              v-bind:key="burger.name"
              v-on:orderedBurger="addToOrder($event)"/>
            </div>
            </section>
            <div id="map_container">
            <h4>Vart du vill mötas upp?</h4>
            <div id="map" v-on:click="setLocation">
              <div v-bind:style="{ left: location.x + 'px', top: location.y + 'px'}" v-bind:key="'dots'">
            T
          </div>
            click here
            </div>
          </div>
      <section>
         <h2>Beställningsinformation</h2>
         <div>
            <h3>Nödvändig Information För Att Skapa Er Vänskap</h3>
            <h4>Ditt Fullständiga Namn</h4>
            <input type="text" v-model="namn" placeholder="För- och Efternamn">
            <h4>Din E-mail</h4>
            <input type="text" v-model="email" placeholder="E-mail">
            <h4>Dubbellkolla att allt ovan stämmer inann du beställer</h4>
            <button v-on:click="orderPressed"> Beställ </button>
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
import menu from '../assets/menu.json'

const socket = io();

let friends =[
  {name: "MysIsak", price: 200, imgSrc: "20211204_004757.jpg", rolig: false, snäll: true},
  {name: "GrönaFaran", price: 250, imgSrc: "20220115_213531.jpg", rolig: true, snäll: false},
  {name: "FruBillys", price: 275, imgSrc: "20220410_122544.jpg", rolig: true, snäll: false},
  {name: "FB-FB", price: 0.25, imgSrcL: "20220402_192541.jpg", rolig: false, snäll: false},
  {name: "TheCutiee", price: 2000, imgSrc: "20220122_011611.jpg", rolig: true, snäll: true},
]

function MenuItem(name, imgSrc, price, rolig, snäll){

}

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu, 
      namn: "",
      orderedBurgers: {},
      location: { x: 0,
            y: 0
          },
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },

    setLocation: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location.x = event.offsetX - 10;
      this.location.y = event.offsetY- 10;
    },

    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location.x =event.offsetX - 10;
      this.location.y =event.offsetY - 10;
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.offsetX - 10,
                                           y: event.offsetY - 10},
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    },

    orderPressed: function (event) {
      let order = {name: this.namn, email: this.email, amountOrdered: this.orderedBurgers}
      console.log(order)
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: this.location.x -10, 
                                           y: this.location.y -10},
                                orderItems: [order.name, order.email, order.amountOrdered]
                              }
                 );
    },
    addToOrder: function (event) {
  this.orderedBurgers[event.name] = event.amount;
},
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
    position: relative;
    margin: 0;
    padding: 0;
    background-repeat: no-repeat;
    width:1920px;
    height: 1078px;
    background: url("../../public/img/polacks.jpg");
    cursor: pointer;
  }
  #map:hover {
    opacity: 0.85;
  }
  #map_container{
    width: 86vw;
    height: 60vh;
    margin: 0%;
    overflow: scroll;
  }
  #map div{
    position: absolute;
    background: black;
    color: white;
    border-radius: 10px;
    width:20px;
    height:20px;
    text-align: center;
  }
  input {
    font-family: Cambria;
  }
</style>