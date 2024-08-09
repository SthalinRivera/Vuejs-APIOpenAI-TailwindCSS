<template>
    <div class="relative w-full h-full">
      <a-scene>
        <a-assets>
          <!-- Cargar imágenes -->
          <img id="city" src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/city.jpg">
          <img id="cubes" src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/cubes.jpg">
          <img id="sechelt" src="https://cdn.aframe.io/360-image-gallery-boilerplate/img/sechelt.jpg">
        </a-assets>
  
        <!-- Sky -->
        <a-sky id="sky" src="#city"></a-sky>
  
        <!-- Botones para cambiar las imágenes del cielo -->
        <a-box position="-1 1.5 -3" color="#FF0000" width="1" height="1" depth="0.1" class="clickable" data-image="#city"></a-box>
        <a-box position="0 1.5 -3" color="#0000FF" width="1" height="1" depth="0.1" class="clickable" data-image="#cubes"></a-box>
        <a-box position="1 1.5 -3" color="#00FF00" width="1" height="1" depth="0.1" class="clickable" data-image="#sechelt"></a-box>
  
        <!-- Cámara -->
        <a-camera>
          <a-cursor></a-cursor>
        </a-camera>
  
      </a-scene>
    </div>
  </template>
  
  <script setup>
  import 'aframe'; // Import A-Frame
  
  // Configurar un listener para eventos de clic en los botones
  const updateSkyImage = (event) => {
    const sky = document.querySelector('#sky');
    const newImage = event.target.getAttribute('data-image');
    if (sky) {
      sky.setAttribute('src', newImage);
    }
  };
  
  document.addEventListener('click', (event) => {
    if (event.target.classList.contains('clickable')) {
      updateSkyImage(event);
    }
  });
  </script>
  
  <style scoped>
  .relative {
    position: relative;
  }
  .w-full {
    width: 100%;
  }
  .h-full {
    height: 100%;
  }
  .clickable {
    cursor: pointer;
  }
  </style>
  