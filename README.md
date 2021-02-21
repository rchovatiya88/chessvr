### Setting up Multiplayer WebXR Chess Game

Open Source WebXR game using aframe.io (webVR framework) Full Code available on Github Page.

Live [Demo](https://chessvr.glitch.me/) - https://chessvr.glitch.me/

#### Pre-Requisties

- Web Browser (Chrome)
- Set up Glitch Account - www.glitch.com

### How it Works

- Add 3D models in GLTF or glb format in the asset folder. Also, you can add any Images, videos, materials in asset folder for reference (Check File Size limit)
- Inside `/public` folder `index.html` is where all the code will go and `/js` folder for all javascript functions / components.

## Goal

Let's define our goal for the project and scene. In order visualize our concept, some of following assets we need

- Environment
- 3D Models of Chess
- Controllers

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

Watch [Tutorial](https://www.youtube.com/watch?v=ktjMCanKNLk&list=PL8MkBHej75fJD-HveDzm4xKrciC5VfYuV)

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

### Step 3

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

### Step 4

- Adding Quest Controllers to move and Teleport in our scene

We import `aframe-teleport-controls` by Fernando Serrano [Github link](https://github.com/fernandojsg/aframe-teleport-controls)

Inside the `<head>` tag we simply copy and past this cdn script

```
    <script src="https://rawgit.com/fernandojsg/aframe-teleport-controls/master/dist/aframe-teleport-controls.min.js"></script>
```

**WARNING**
`The implementation for quest controllers doesn't quite work from the github page.`

Luckily [Takashi Yoshinaga](https://github.com/TakashiYoshinaga) create a great implementation and showed how to implement in his demo - `https://quest-demo.glitch.me`
![Demo](https://im2.ezgif.com/tmp/ezgif-2-f1d0dd3fd324.gif)

Using Takashi implementation, since we already imported the `aframe-teleport` we add cameraRig entity

```
 <a-entity id="cameraRig">
            <a-entity id="head" camera wasd-controls look-controls position="0 1.6 0">
            </a-entity>
            <a-entity id="ctlL"
                teleport-controls="cameraRig: #cameraRig; teleportOrigin: #head; startEvents: teleportstart; endEvents: teleportend"
                raycaster="objects: .collidable; far:1.2; " oculus-touch-controls="hand: left" input-listen>
                <a-text value="Press and let go \nX: to Move" position="0 0.08 0"
                    rotation="-90 0 0" scale="0.1 0.1 0.1" align="center" color="#FFFFFF"></a-text>
              <a-sphere radius="0.01" position="0 0 -1.2" color="#FFFFFF"></a-sphere>
            </a-entity>
            <a-entity id="ctlR" raycaster="objects: .collidable; far:1.2; " oculus-touch-controls="hand: right" input-listen>
                <a-text value="Use Grip to interact"
                    position="0 0.08 0" rotation="-90 0 0" scale="0.1 0.1 0.1" align="center" color="#FFFFFF"></a-text>
              <a-sphere radius="0.01" position="0 0 -1.2" color="#FFFFFF"></a-sphere>
            </a-entity>
        </a-entity>
```

And we need to add EventListener script

```
<script>
    AFRAME.registerComponent('input-listen', {
        init:
            function () {
                //Declaration and initialization of flag
                //which exprains grip button is pressed or not.
                //"this.el" reffers ctlR or L in this function
                this.el.grip = false;



                //Grip Pressed
                this.el.addEventListener('gripdown', function (e) {
                    //Setting grip flag as true.
                    this.grip = true;
                });
                //Grip Released
                this.el.addEventListener('gripup', function (e) {
                    //Setting grip flag as false.
                    this.grip = false;
                });

                //Raycaster intersected with something.
                this.el.addEventListener('raycaster-intersection', function (e) {
                    //Store first selected object as selectedObj
                    this.selectedObj = e.detail.els[0];
                });
                //Raycaster intersection is finished.
                this.el.addEventListener('raycaster-intersection-cleared', function (e) {
                    //Clear information of selectedObj
                    this.selectedObj = null;
                });

                //A-buttorn Pressed
                this.el.addEventListener('abuttondown', function (e) {
                       //Start pointing position to teleport
                    this.emit('teleportstart');
                });
               this.el.addEventListener('abuttonup', function (e) {
                    //Jump to pointed position
                    this.emit('teleportend');
                });

                //X-buttorn Pressed
                this.el.addEventListener('xbuttondown', function (e) {
                    //Start pointing position to teleport
                    this.emit('teleportstart');
                });

                //X-buttorn Released
                this.el.addEventListener('xbuttonup', function (e) {
                    //Jump to pointed position
                    this.emit('teleportend');
                });

                //console.log(this);
            },

        //called evry frame.
        tick: function () {

            if (!this.el.selectedObj) { return; }
            if (!this.el.grip) { return; }

            //Getting raycaster component which is attatched to ctlR or L
            //this.el means entity of ctlR or L in this function.
            var ray = this.el.getAttribute("raycaster").direction;
            //setting tip of raycaster as 1.1m forward of controller.
            var p = new THREE.Vector3(ray.x, ray.y, ray.z);
            p.normalize();
            p.multiplyScalar(1.2);
            //Convert local position into world coordinate.
            this.el.object3D.localToWorld(p);
            //Move selected object to follow the tip of raycaster.
            this.el.selectedObj.object3D.position.set(p.x, p.y, p.z);
        }
    });


</script>
```

![Step 4](https://cdn.glitch.com/97890fbd-889b-466f-a357-23627a83de50%2Fdemogif.gif?v=1613756972311)

### Adding Hands and phsyics

Since we need to add hands and being able to pick up chess pieces we need `aframe-physics` and `hands` - @[Will Murphy](https://github.com/wmurphyrd) to the rescue with `aframe-super-hands-component`

Also - Kyle Baker helped us simplify the implementation - > https://github.com/wmurphyrd/aframe-super-hands-component/issues/188

Per Kyle instruction 
 - Import the components in head 
    ```
     <script src="https://unpkg.com/super-hands/dist/super-hands.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/n5ro/aframe-physics-system@v4.0.1/dist/aframe-physics-system.js"></script>
    <script src="https://unpkg.com/aframe-event-set-component@^4.1.1/dist/aframe-event-set-component.min.js"></script>
    <script src="https://unpkg.com/aframe-physics-extras/dist/aframe-physics-extras.min.js"></script>
    ```
    
- Then add Script 
```
<script>
      AFRAME.registerComponent("phase-shift", {
        init: function() {
          var el = this.el;
          el.addEventListener("gripdown", function() {
            el.setAttribute("collision-filter", { collisionForces: true });
          });
          el.addEventListener("gripup", function() {
            el.setAttribute("collision-filter", { collisionForces: false });
          });
        }
      });
    </script>
  ```
  
  - Add Mixin inside your `<assets>` tag 
  
  ```
    <a-mixin
          id="all-interactions"
          hoverable
          grabbable
          stretchable
          draggable
          event-set__hoveron="_event: hover-start; material.opacity: 0.7; transparent: true"
          event-set__hoveroff="_event: hover-end; material.opacity: 1; transparent: false"
          dynamic-body
        ></a-mixin>

        <a-mixin
          id="grab-move"
          hoverable
          grabbable
          draggable
          event-set__hoveron="_event: hover-start; material.opacity: 0.7; transparent: true"
          event-set__hoveroff="_event: hover-end; material.opacity: 1; transparent: false"
          dynamic-body="shape: box; sphereRadius: 0.1"
        ></a-mixin>

        <a-mixin
          id="physics-hands"
          physics-collider
          phase-shift
          collision-filter="collisionForces: false"
          static-body="shape: sphere; sphereRadius: 0.02"
          super-hands="colliderEvent: collisions;
                              colliderEventProperty: els;
                              colliderEndEvent: collisions;
                              colliderEndEventProperty: clearedEls;"
        ></a-mixin>
  
  ```
  
  - Now we need to tell our models to get mixins
  ```
  <a-gltf-model
        mixin="all-interactions"
        class="collidable"
        src="#knight"
        scale="0.03 0.03 0.03"
        position="-0.38701 1.08131 -2.44533"
      >
      </a-gltf-model>
      <a-gltf-model
        mixin="all-interactions"
        src="#queen"
        scale="0.03 0.03 0.03"
        position="0.07661 1.08131 -2.44533"
      >
  ```
  
  - Lastly we need to mixin, hands and script to the CameraRig
  
  ```
  <a-entity
          id="ctlL"
          teleport-controls="cameraRig: #cameraRig; teleportOrigin: #head; startEvents: teleportstart; endEvents: teleportend"
          raycaster="objects: .collidable; far:1.2; "
          hand-controls="hand: left" 
          mixin="physics-hands" <-updated
          input-listen
          phase-shift <- updated
        >
  ```
  
  
# TODO

- Adding `aframe-physics` to interact with chess pieces
- Multiplayer
