<template>
    <div>
      <img v-binds:src="burger.URL">
      {{ burger.name }} {{ burger.kCal }}   <!-- Fyll på med det som ska visas?-->
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
  
  </style>
  