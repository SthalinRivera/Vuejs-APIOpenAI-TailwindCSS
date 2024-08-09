<template>
 <a-scene embedded arjs='sourceType: webcam;'>
    <a-marker preset="hiro">
      <!-- Usamos un proxy CORS para evitar problemas de origen cruzado -->
      <a-entity
        position="0 0 0"
        scale="0.05 0.05 0.05"
        gltf-model="https://raw.githack.com/AR-js-org/AR.js/master/aframe/examples/image-tracking/nft/trex/scene.gltf"
      ></a-entity>
    </a-marker>
    <a-entity camera></a-entity>
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