<template>
            <div class="menuitem">
            <h3>{{ burger.name }}</h3>
            <img class="image" v-bind:src="burger.imgSrc">
            <footer>
               <div class="description">
                  <p>Rolig: {{ burger.rolig }}</p>
                  <p>Snäll: {{ burger.snäll }}</p>
                  <p>Pris: {{ burger.price }}SEK</p>
                  Amount: <button v-on:click="decreaseAmount"> - </button> {{ amountOrdered }} <button v-on:click="increaseAmount"> + </button>
               </div>
             </footer>
             </div>
  </template>
  
  <script>
  export default {
   data: function () {
  return {
    amountOrdered: 0,
  }
},
    name: 'OneBurger',
    props: {
      burger: Object
    },
    methods: {
    decreaseAmount: function (event) {
      if (this.amountOrdered > 0) {this.amountOrdered = this.amountOrdered - 1;}
    this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              
    });
  },
    increaseAmount: function (event) {
      this.amountOrdered++;
    this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              
    });
  },
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
  