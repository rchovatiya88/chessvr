### Setting up Multiplayer WebXR Chess Game

Open Source WebXR game using aframe.io (webVR framework) Full Code available on our Github Page.

#### Pre-Requisties

- Set up Glitch Account - www.glitch.com
- If you want to Improve this experience

  - Create a pull request on this Github

### How it Works

- Add 3D models in GLTF or glb format in the asset folder. Also, you can add any Images, videos, materials in asset folder for reference (Check File Size limit)
- Inside `/public` folder `index.html` is where all the code will go and `/js` folder for all javascript functions / components.

## Goal

Let's define our goal for the project and scene. In order visualize our concept, some of following assets we need

- Environment
- 3D Models of Chess
- Ground

### Creating a Scene

Similar to normal Web HTML Pages. We have

- `<head>` tag (To import all our dependencies)
- `<body>` tag(All entities and assets)

### Step 1

- Let's set up our floor / ground

In a-frame, we can define a `<a-plane>`

For example we can follow the docs from a-frame [Getting Started](https://aframe.io/docs/1.1.0/introduction/)

```js
<a-plane
  position="0 0 -4"
  rotation="-90 0 0"
  width="4"
  height="4"
  color="#7BC8A4"
></a-plane>
```

- For our project we need a real ground, We decided use a [Ground texture](https://www.textures.com/browse/streets/97701)
  ![Ground textured](https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2FTexturesCom_FloorStreets0064_2_M.jpg?v=1612300231287)

```js
<html>
  <head>
    <title>Chess VR - Let's play chess in WEBXR</title>
    <script src="https://aframe.io/releases/1.1.0/aframe.min.js"></script>
  </head>

  <body>
    <a-scene>
      <a-assets>
        <img
          id="ground"
          src="https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2FTexturesCom_Carpet0020_1_seamless_S.jpg?v=1612295412711"
        />
      </a-assets>

      <!-- Ground -->
      <a-plane
        material="color: #FFFFFFF; src: #ground; repeat : 5 5;"
        rotation="-90 0 0"
        scale="10 10 1"
      >
      </a-plane>
    </a-scene>
  </body>
</html>
```

![Step 1](https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2FScreen%20Shot%202021-02-02%20at%203.12.33%20PM.png?v=1612296769130)

### Step 2

- Let's add a open-source `aframe-environment compoment` from [Diego F. Goberna](https://github.com/feiss/aframe-environment-component/) to easily create background scene for us!

![Scene Examples](https://github.com/feiss/aframe-environment-component/raw/master/assets/aframeenvironment.gif?raw=true)

We used a `environment="preset forest"` forest envrionement but we can do a bit more to add more customization to match our scene. For example, adding and removing different aspects of the scene

```js
    <!-- Environment -->
      <a-entity
        environment="preset:  forest;  playArea:  2;  active:  true;  seed:  8;
                     skyType:  gradient;
                     skyColor:  #ffffff;  // Change the color of the sky
                     horizonColor:  #87CEEB;
                     fog:  0.5;
                     groundYScale:  4.18;  groundTexture:  squares;  groundColor:  #43994b;  //Change ground color
                     groundColor2:  #43994b;  dressing:  trees;  dressingAmount:  500;
                     dressingColor:  #43994b;  dressingScale:  1;
                     gridColor:  #43994b"
      ></a-entity>
```

[View docs for more info](https://github.com/feiss/aframe-environment-component/)

_A Tip to easily change parameters_

- Use [A-frame Inspector](https://github.com/aframevr/aframe-inspector) Please `ctrl+alt+i` on a scene and it will open an inspector, then on the right side change the parameter. Copy the changes and paste it to your html.

![Step 2](https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2FScreen%20Shot%202021-02-02%20at%204.26.32%20PM.png?v=1612301609061)

### 3

- Let's add 3d Objects, we can use models our custom assets or use [Sketchfab](https://sketchfab.com/feed)

We have a bench and our chess board, For WebVR we need `.gltf` or `.glb`file

Similar to the code from [aframe docs](https://aframe.io/docs/1.1.0/primitives/a-gltf-model.html#sidebar)

```js
<a-scene>
  <a-assets>
    <a-asset-item id="tree" src="tree.gltf"></a-asset-item>
  </a-assets>

  <!-- Using the asset management system. -->
  <a-gltf-model src="#tree"></a-gltf-model>

  <!-- Defining the URL inline. Not recommended but more comfortable for web developers. -->
  <a-gltf-model src="tree.gltf"></a-gltf-model>
</a-scene>
```

- By using the `Aframe inspector` we position each chess pieces into proper spaces

![Step 3](https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2FScreen%20Shot%202021-02-02%20at%205.44.21%20PM.png?v=1612305923293)

# TODO

- Adding motion joystick
- Interactions
