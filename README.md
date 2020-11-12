### Setting up Multiplayer WebXR Chess Game

Open Source WebXR game using aframe.io (webVR framework) Full Code available on our Github Page.

#### Pre-Requisties

- Set up Glitch Account - www.glitch.com
- If you want to Improve this experience

  - Create a pull request on this Githup

### How it Works

- Add 3D models in GLTF or glb format in the asset folder. Also, you can add any Images, videos, materials in asset folder for reference (Check File Size limit)
- Inside `/public` folder `index.html` is where all the code will go and `/js` folder for all javascript functions / components.

### Creating a Scene

```js
<html>
  //COMMENTS - Top HTML tag
  <head>
 
    // In HEAD tag import various js libraries
    <script src="https://aframe.io/releases/1.0.4/aframe.min.js"></script> // Importing
    aframe
    <script src="https://unpkg.com/aframe-environment-component@1.1.0/dist/aframe-environment-component.min.js"></script>
    // Importing evnvironment component that will help create various pre made scenes.
  </head>
  <body>
    <a-scene environment="preset: checkerboard; groundColor: #FFF">
     
      <a-sky color="#87ceeb"></a-sky>
      
    </a-scene>
  </body>
</html>
```

