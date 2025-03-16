---
title: "Three.js"
description: ""
summary: ""
date: 2024-10-21T20:09:40+08:00
lastmod: 2024-10-21T20:09:40+08:00
draft: false
weight: 105
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/three.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Three.js is a rich JavaScript library for computer graphics representation on browser using WebGL. Visit their [documentation](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene) and [examples](https://threejs.org/examples/#webgl_animation_keyframes) top understand better.

### Computer Graphics Concepts

#### Vertex

A vertex is a point in 3D space, defined by its x, y, and z coordinates. Multiple vertices are used to create polygons or meshes that form the geometry of 3D objects.

#### Rasterization

The process of converting 3D models into a 2D image by mapping the 3D scene onto a 2D viewport (like your screen). This step converts polygons into pixels or fragments.

#### Texture

Textures are images applied to the surface of a geometry to give it more detail or realism (e.g., brick textures on a wall). You can use textures for color, bump mapping, or normal mapping to create the illusion of depth.

#### Shaders

Shaders are small programs that run on the GPU (Graphics Processing Unit) to control how vertices and pixels are processed and rendered.

- Vertex Shader: Transforms 3D coordinates into 2D screen coordinates
- Fragment/Pixel Shader: Determines the color and appearance of individual pixels

#### Light Tracing

A form of ray tracing, where light rays are simulated as they interact with surfaces. Light tracing focuses on how light enters the scene from various sources and is traced through multiple reflections and refractions for realistic lighting effects.

### Three.js Common Components

#### Getting started

Install Three.js developement kit, import or link the CDN to use Three.js

```js {title="javascript"}
import * as THREE from "https://cdn.skypack.dev/three@0.132.2";
import { OrbitControls } from "https://cdn.skypack.dev/three@0.132.2/examples/jsm/controls/OrbitControls.js";
```

```html {title="html"}
<script type="importmap">
  {
    "imports": {
      "three": "https://cdn.jsdelivr.net/npm/three@0.163.0/build/three.module.js",
      "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.163.0/examples/jsm/"
    }
  }
</script>
```

```html
<script type="module" src="example.js">
  // Three JS goes here without 'src' attribute
</script>
```

{{< callout note >}} The example code below includes many elements in detail and is long {{< /callout >}}

{{< details "Example Three.js Code" >}}

```js {title="example.js"}
import * as THREE from "https://cdn.skypack.dev/three@0.132.2";
import { OrbitControls } from "https://cdn.skypack.dev/three@0.132.2/examples/jsm/controls/OrbitControls.js";

const scene = new THREE.Scene();

const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.set(15, 16, 13);
camera.lookAt(scene.position);

const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.shadowMapEnabled = true;   // Enable Shadow
document.body.appendChild(renderer.domElement);

const controls = new OrbitControls(camera, renderer.domElement);
controls.update();

// Geometry + Material = Mesh
const planeGeometry = new THREE.PlaneGeometry(20, 20);
const planeMaterial = new THREE.MeshPhongMaterial({ color: 0xcccccc, side: THREE.DoubleSide });
const plane = new THREE.Mesh(planeGeometry, planeMaterial);
plane.receiveShadow = true;
plane.rotation.x = -0.5 * Math.PI;
plane.position.y = 0;
scene.add(plane);

const colors = [0xff0000, 0x0088aa, 0xaaaaaa, 0xdddd00]; // Red, blue, grey, yellow
const cl = colors.length;

const materials = [
    new THREE.MeshBasicMaterial({ side: THREE.DoubleSide }),
    new THREE.MeshPhongMaterial({
        specular: 0xffffff, shininess: 100,
        side: THREE.DoubleSide // for drawing the inside of the tube
    }),
    new THREE.MeshStandardMaterial({
        metalness: 0.9, roughness: 0.4,
        side: THREE.DoubleSide
    }),
    new THREE.MeshLambertMaterial({
        wireframe: true, wireframeLinewidth: 2,
        side: THREE.DoubleSide
    })
];
const ml = materials.length;

const geometries = [
    new THREE.SphereGeometry(1, 16, 8),
    new THREE.ConeGeometry(1, 2, 16),
    new THREE.BoxGeometry(1.5, 1.5, 1.5),
    new THREE.CylinderGeometry(1, 1, 2, 16),
    new THREE.RingGeometry(0.3, 1, 16),
    new THREE.TorusGeometry(1, 0.5, 16, 16),
    new THREE.TorusKnotGeometry(1, 0.3, 128, 8),
    new THREE.IcosahedronGeometry(1),
    new THREE.DodecahedronGeometry(1),
    new THREE.OctahedronGeometry(1),
    new THREE.TetrahedronGeometry(1),
    // new THREE.CapsuleGeometry(1, 1, 4, 16)
    // Custom geometries:
    // EdgesGeometry
    // ExtrudeGeometry: create 3D using 2D shape
    // LatheGeometry: based on f(x) on x axis
    // PolyhedronGeometry: specifying vertexs
    // ShapeGeometry: create 2D shape
    // TubeGeometry: extrude along 3D curve
    // WireframeGeometry: create 2D shape
]

var items = []
for (let i = 0; i < 4; i++) {
    for (let j = 0; j < 4; j++) {
        var geometry = geometries[(i * 4 + j) % geometries.length];
        var material = materials[rand(ml)];
        var item = new THREE.Mesh(geometry, material);
        var pos = grid_pos(i, j);
        item.position.set(pos[0], pos[1], pos[2]);
        item.material.color.set(colors[rand(cl)]);
        item.castShadow = true;
        scene.add(item);
        items.push(item);
    }
}

const distance = 50;
const angle = Math.PI / 16;
const penumbra = 0.5;
const decay = 0.1;

const spotLight = new THREE.SpotLight(0xffffff, 1, distance, angle, penumbra, decay);
spotLight.position.set(10, 20, -20);
spotLight.castShadow = true;
scene.add(spotLight);

const ambientLight = new THREE.AmbientLight(0x101010);
scene.add(ambientLight);

const directionalLight = new THREE.DirectionalLight(0x886200, 1);
directionalLight.position.set(10, 20, 20);
directionalLight.castShadow = true;
scene.add(directionalLight);

// const hemisphereLight = new THREE.HemisphereLight(0x4040ff, 0xffff80, 1.0);
// hemisphereLight.position.set(-10, 20, 20);
// hemisphereLight.castShadow = true;
// scene.add(hemisphereLight);

const light = new THREE.PointLight(0xE11584, 1, 100);
light.position.set(0, 5, 0);
light.castShadow = true;
scene.add(light);

const rectAreaLight = new THREE.RectAreaLight(0xff0000, 1.0, 200, 200);
rectAreaLight.position.set(-10, 20, -20);
rectAreaLight.lookAt(0, 0, 0);
scene.add(rectAreaLight);


const gridHelper = new THREE.GridHelper(10, 10);
scene.add(gridHelper);

const yGrid = new THREE.GridHelper(10, 10);
yGrid.rotation.x = Math.PI / 2; // Rotate the grid to align with the Y-axis
scene.add(yGrid);

const axesHelper = new THREE.AxesHelper(5);
scene.add(axesHelper);

const cameraHelper = new THREE.CameraHelper(camera);
scene.add(cameraHelper);

const spotLightHelper = new THREE.SpotLightHelper(spotLight);
scene.add(spotLightHelper);

const directionalLightHelper = new THREE.DirectionalLightHelper(directionalLight, 5);
scene.add(directionalLightHelper);

const pointLightHelper = new THREE.PointLightHelper(light);
scene.add(pointLightHelper);

var ypos = [];
for (let i = 0; i < 16; i++) {
    ypos.push(Math.random());
}

var animate = function () {
  requestAnimationFrame(animate);
  // required if controls.enableDamping or controls.autoRotate are set to true

  var time = performance.now() * 0.001; // Get current time in seconds
  var amplitude = 1;
  var frequency = 1;
  for (var i = 0; i < items.length; i++) {
      var yOffset = 2 + Math.sin(time * frequency + ypos[i] * 10) * amplitude; // Calculate y offset based on sine function
      items[i].rotation.y += 0.01;
      items[i].position.y = yOffset;
  }

  controls.update();
  renderer.render(scene, camera);
}

function grid_pos(x, y) {
  return [(x - 2) * 4 + 2, 1, (y - 2) * 4 + 2];
}

function rand(n) {
  return Math.floor(Math.random() * n);
}

function handleResize() {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
}

animate();
window.addEventListener('resize', handleResize, false);
```

{{< /details >}}

Results

<iframe src="three/index.html" width="100%" height="600" style="border:none;"></iframe>

#### Geometry

Geometry defines the shape of the 3D object through vertices, faces, and edges.

#### Material

Materials define how the surface of a mesh looks when rendered, including its color, reflectivity, texture, and lighting response.

| Material | Description |
| - | - |
| MeshBasicMaterial | A material that doesn’t react to light |
| MeshStandardMaterial | Supports lighting and reflections, used for realistic rendering |
| MeshPhongMaterial | Includes specular highlights for shiny surfaces |
| MeshLambertMaterial | For non-shiny surfaces, without specular highlights |
| MeshNormalMaterial | Maps the normal vectors to RGB colors |
| MeshPhysicalMaterial | Extension of the MeshStandardMaterial, providing more advanced physically-based rendering properties |
| MeshDepthMaterial | The closer to the camera, the brigther it is |
| MeshToonMaterial | A material implementing toon shading |

#### Helper

Helper helps visualize light, directions, camera and position of elements.

#### Light

| Types | Description |
| - | - |
| AmbientLight | General light that illuminates all objects equally |
| DirectionalLight | Like sunlight, casts parallel rays from a specific direction |
| HemisphereLight | Different light source from sky and ground |
| PointLight | A light that emits in all directions from a point (like a light bulb) |
| SpotLight | A cone-shaped light that shines in a specific direction |
| RectAreaLight | Simulate light source from a window |

#### Loader

User loader to load tools into the model

```js {title="example.js"}
const textureLoader = new THREE.TextureLoader();
const texture = textureLoader.load('path/to/texture.jpg');
const material = new THREE.MeshBasicMaterial({ map: texture });
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);
```

### Amazing Three.js examples

![Reflection](images/reflection.png)

{{< card-grid >}}
  {{< link-card title="Little Tokyo" href="https://threejs.org/examples/#webgl_animation_keyframes" >}}
  {{< link-card title="Material Car Ferrari" href="https://threejs.org/examples/#webgl_materials_car" >}}
  {{< link-card title="Equirectangular" href="https://threejs.org/examples/#webgpu_pmrem_equirectangular" >}}
{{< /card-grid >}}
{{< card-grid >}}
  {{< link-card title="Mirror" href="https://threejs.org/examples/#webgpu_mirror" >}}
  {{< link-card title="Games FPS" href="https://threejs.org/examples/#games_fps" >}}
  {{< link-card title="Physics Terrain" href="https://threejs.org/examples/#physics_ammo_terrain" >}}
{{< /card-grid >}}
{{< card-grid >}}
  {{< link-card title="Misc Exporter" href="https://threejs.org/examples/#misc_exporter_ply" >}}
  {{< link-card title="Periodic Table" href="https://threejs.org/examples/#css3d_periodictable" >}}
  {{< link-card title="3D Sprites" href="https://threejs.org/examples/#css3d_sprites" >}}
{{< /card-grid >}}
{{< card-grid >}}
  {{< link-card title="Youtube Cube" href="https://threejs.org/examples/#css3d_youtube" >}}
  {{< link-card title="Light Probe" href="https://threejs.org/examples/webgl_lightprobe.html" >}}
  {{< link-card title="Geometry Colors" href="https://threejs.org/examples/#webgl_geometry_colors" >}}
{{< /card-grid >}}

### Advanced Applications

#### Procedual-GL.js

[Procedural GL JS](https://www.procedural.eu/) is a library for creating 3D map experiences on the web, written in JavaScript and WebGL. It is built on top of THREE.js.

#### Path Tracing

[This](https://erichlof.github.io/THREE.js-PathTracing-Renderer/) is an amzing real-time PathTracing with global illumination and progressive rendering, all on top of the Three.js WebGL framework.
