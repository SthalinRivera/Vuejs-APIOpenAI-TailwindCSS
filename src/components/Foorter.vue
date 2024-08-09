<template>
    <a-scene embedded arjs='sourceType: webcam;'>
      <!-- Definición del marcador -->
      <a-marker preset="hiro">
        <a-box position='0 0.5 0' material='color: red;'></a-box>
      </a-marker>
      
      <!-- La cámara AR -->
      <a-entity camera class="h-screen w-full"></a-entity>
    </a-scene>
  </template>
  
  <script setup>
    // Puedes agregar lógica aquí si es necesario
  </script>
  
  <style scoped>
    /* Ajusta el tamaño del canvas para la AR */
 
  </style>