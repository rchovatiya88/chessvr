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
    <a-scene environment="preset: checkerboard; groundColor: #FFF">  // this is to change the scene   
   <a-sky color="#87ceeb"></a-sky>
      
    <a-assets>
        <!--     All the Assets inside <a-assets> TAG</a-assets> -->
        <!--      Like a BOX <a-box position="0 1 -5" rotation="45 45 45" color="#4CC309"></a-box> -->
<!--         Insert CDN URLlocation of the 3D obects (Must be glb or gltf format) -->
        <a-asset-item 
          id="chessboard"
          src="https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2Fout%20(1).glb?v=1604949268125"
        ></a-asset-item>
      </a-assets>
    
    </a-scene>
  </body>
</html>
```


# TODO 
[] Adding motion joystick 
[] Interactions
[] Individual
[] Handtracking
[] Add individual assets 
[] physics for assets