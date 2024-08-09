<template>
    <div ref="container" style="width: 100vw; height: 100vh; margin: 0; overflow: hidden;"></div>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
  import * as THREE from 'three';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  import { RGBELoader } from 'three/examples/jsm/loaders/RGBELoader.js';
  
  const container = ref(null);
  let renderer, scene, camera, controls;
  
  onMounted(async () => {
    await init();
  });
  
  onUnmounted(() => {
    if (renderer) renderer.dispose();
    if (controls) controls.dispose();
  });
  
  async function init() {
    // Create renderer
    renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setAnimationLoop(animate);
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.toneMapping = THREE.ACESFilmicToneMapping;
    container.value.appendChild(renderer.domElement);
  
    // Create scene
    scene = new THREE.Scene();
  
    // Create camera
    camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 0.05, 20);
    camera.position.set(0.35, 0.05, 0.35);
  
    // Add controls
    controls = new OrbitControls(camera, renderer.domElement);
    controls.autoRotate = true;
    controls.autoRotateSpeed = -0.5;
    controls.target.set(0, 0.2, 0);
    controls.update();
  
    // Load environment texture and model
    const rgbeLoader = new RGBELoader().setPath('/textures/equirectangular/');
    const gltfLoader = new GLTFLoader().setPath('/textures/equirectangular/');
  
    const [texture, gltf] = await Promise.all([
      rgbeLoader.loadAsync('venice_sunset_1k.hdr'),
      gltfLoader.loadAsync('IridescenceLamp.glb'),
    ]);
  
    // Setup environment
    texture.mapping = THREE.EquirectangularReflectionMapping;
    scene.background = texture;
    scene.environment = texture;
  
    // Add model to scene
    scene.add(gltf.scene);
  
    // Handle window resize
    window.addEventListener('resize', onWindowResize);
  }
  
  function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
  }
  
  function animate() {
    controls.update(); // Update controls
    renderer.render(scene, camera);
  }
  </script>
  
  <style scoped>
  /* Add any specific styles if needed */
  </style>
  