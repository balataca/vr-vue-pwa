<template>
  <a-scene
    stats 
    inspector
    renderer="antialias: false;
              colorManagement: false;
              sortObjects: true;
              physicallyCorrectLights: false;
              maxCanvasWidth: 1280;
              maxCanvasHeight: 1280;"
  >
    <a-assets>
      <img id="sky" src="static_assets/images/sky.jpeg">
      <a-asset-item id="city-model" src="static_assets/models/city/city.glb"></a-asset-item>
      <a-asset-item id="car-model" src="static_assets/models/car/scene.gltf"></a-asset-item>
      <a-asset-item id="truck-model" src="static_assets/models/truck/truck.glb"></a-asset-item>
      <a-asset-item id="traffic-sign-model" src="static_assets/models/traffic_sign/scene.gltf"></a-asset-item>
    </a-assets>

    <!-- Camera -->
    <a-entity
      id="camera1"
      camera="active: true"
      look-controls
      wasd-controls
      position="5.02497 1.6 4.5329"
      rotation="0 37 0"
    >
      <a-entity
        cursor="fuse: true; fuseTimeout: 500"
        position="0 0 -1"
        geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
        material="color: #fff; shader: flat"
      >
      </a-entity>
    </a-entity>

    <!-- City -->
    <a-entity
      id="city"
      gltf-model="url(static_assets/models/city/city.glb)"
      position="0 -0.1 0"
      scale="1 1 1"
      shadow="cast: true; receive: true;"
    ></a-entity>

    <!-- Billboard -->
    <a-text
      id="billboard"
      geometry="primitive: plane; width: 2; height: 1;"
      material="color: blue;"
      align="center"
      color="#000"
      value="Start"
      position="3.26134 3 2.2635"
      look-at="[camera]"
    ></a-text>

    <!-- Traffic Sign -->
    <a-entity
      id="traffic-sign" rotation="0 -90 0"
      gltf-model="url(static_assets/models/traffic_sign/scene.gltf)"
      position="-5.8149 0.1 4.26463"
      scale=".01 .01 .01"
      shadow="cast: true; receive: true;"
    >
    </a-entity>

    <!-- Truck -->
    <a-entity
      id="truck"
      ref="truck"
      gltf-model="url(static_assets/models/truck/truck.glb)"
      position="-3 0.10796 -16.97038"
      scale="1 1 1"
      dynamic-body="shape: box; mass: 10;"
      shadow="cast: true; receive: true;"
    ></a-entity>

    <!-- Car -->
    <a-entity
      id="car"
      ref="car"
      gltf-model="url(static_assets/models/car/scene.gltf)"
      position="-11 0.1 1.4"
      rotation="0 96 0"
      scale="1 1 1"
      dynamic-body="shape: box; mass: 2;"
      shadow="cast: true; receive: true;"
      sound="src: url(static_assets/sounds/car_crash.mp3);"
    ></a-entity>

    <!-- Lights -->
    <a-entity light="type: ambient; color: #BBB; intensity: 1;"></a-entity>
    <a-entity
      id="sun"
      light="type: directional; 
             distance: 100; 
             color: #b7815b; 
             intensity: .5; 
             angle: 60; 
             castShadow: true; 
             target: #city; 
             shadowCameraTop: 20;
             shadowCameraBottom: -20;
             shadowCameraRight: 50;
             shadowCameraLeft: -50;
             shadowCameraFov: 90;"
      position="-47.00783 40 -14.42622"
      target="#city"
    ></a-entity>

    <!-- Background sky. -->
    <a-sky height="2048" radius="60" src="url(static_assets/images/sky.jpeg)" theta-length="170" width="2048"></a-sky>

    <!-- Ground. -->
    <a-plane
      color="#4d4d4d"
      width="120"
      height="120"
      rotation="-90 0 0"
      static-body
      shadow="cast: true; receive: true;"
    ></a-plane>
  </a-scene>
</template>

<script>
import 'aframe'
import 'aframe-physics-system'
import 'aframe-look-at-component'

export default {
  name: 'CarCrash',
  data () {
    return {
      started: false
    }
  }
}
</script>
