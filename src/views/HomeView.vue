<template>
  <div>
    <div>
      Burgers
      <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"/>
    </div>
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
  {name: "MysIsak", URL: "20211204_004757.jpg", kCal: "Mysig", gluten_lactose: "Rolig"},
  {name: "GrönaFaran", URL: "20220115_213531.jpg", kCal: "Livlig", gluten_lactose: "Stark -kolla in biccarna-"},
  {name: "FruBillys", URL: "20220410_122544.jpg", kCal: "Har alltid med sig Billys", gluten_lactose: "Stylish"},
  {name: "FB-FB", URL: "20220402_192541.jpg", kCal: "Tar alltid med sig festen", gluten_lactose: "Försvinner i dimman"},
  {name: "TheCutiee", URL: "20220122_011611.jpg", kCal: "Gullig", gluten_lactose: "Bästa snusvännen"},
]

function MenuItem(name, URL, kCal, gluten_lactose){

}

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: friends
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
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }
</style>