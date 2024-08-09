<template>
    <a-scene>
      <a-sky src="/360/img01.jpg" rotation="0 -130 0"></a-sky>
      <a-text font="kelsonsans" value="Puy de Sancy, France" width="6" position="-2.5 0.25 -1.5" rotation="0 15 0"></a-text>
    </a-scene>
  </template>
  
  <script setup>
  import 'aframe'; // Import A-Frame
  </script>
  
  <style scoped>
  /* Add any specific styles if needed */
  a-scene {
    width: 100vw;
    height: 100vh;
  }
  </style>
  