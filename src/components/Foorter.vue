<template>
    <a-scene embedded arjs='sourceType: webcam;'>
      <!-- Definición del marcador -->
      <a-marker preset="hiro">
        <a-box position='0 0.5 0' material='color: red;'></a-box>
      </a-marker>
      
      <!-- La cámara AR -->
      <a-entity camera ></a-entity>
    </a-scene>
  </template>
  
  <script setup>
    // Puedes agregar lógica aquí si es necesario
  </script>
  
  <style scoped>
  /* Ajusta el tamaño del canvas para la AR */
  a-scene {
    width: 100vw;
    height: 100vh;
    margin: 0;
    overflow: hidden;
  }

  /* Asegúrate de que la cámara esté centrada */
  a-entity[camera] {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
  }

  /* Opcional: estiliza el marcador si es necesario */
  a-marker {
    width: 100%;
    height: 100%;
  }
</style>