# Merchandise 3D Customizer - Unified UI Pattern

**Products**: Mug (3-Zone, Full Wrap, Heart Handle), Tumbler, Bottle
**Style**: Bold & Colorful
**Priority**: Mobile-First
**Date**: 2026-02-03

---

## Overview

Unified 3D preview component that works across all merchandise products. Same interaction patterns, different 3D models and zone configurations.

---

## Product Configurations

| Product | Zones | 3D Model | Special Features |
|---------|-------|----------|------------------|
| Mug (3-Zone) | Front, Back, Rear | mug-standard.glb | 3 independent zones |
| Mug (Full Wrap) | Single wrap | mug-standard.glb | Continuous image |
| Mug (Heart Handle) | Front, Back | mug-heart.glb | Handle color picker |
| Tumbler | Front, Back | tumbler.glb | Lid color option |
| Bottle | Front, Back | bottle.glb | Cap color option |

---

## Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Customize Your [Product]     │  ← Header
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │      ┌─────────────┐      │  │
│  │      │             │      │  │
│  │      │   3D Model  │      │  │  ← 3D Preview
│  │      │  (rotatable)│      │  │     (touch to rotate)
│  │      │             │      │  │
│  │      └─────────────┘      │  │
│  │                           │  │
│  │   ↻ Drag to rotate        │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  ┌───────┬────────┬─────────┐   │  ← Zone Tabs
│  │ FRONT │  BACK  │  REAR   │   │
│  │   ●   │        │         │   │
│  └───────┴────────┴─────────┘   │
├─────────────────────────────────┤
│                                 │
│  📷 ADD IMAGE                   │
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │   ☁️  Drag & drop or      │  │  ← Upload Zone
│  │       tap to browse       │  │
│  │                           │  │
│  │   PNG, JPG, PDF (10MB)    │  │
│  └───────────────────────────┘  │
│                                 │
│  ✏️ ADD TEXT                    │
│  ┌───────────────────────────┐  │
│  │ + Add text layer          │  │  ← Text Layers
│  └───────────────────────────┘  │
│                                 │
├─────────────────────────────────┤
│  💰 $25.00    [🛒 ADD TO CART]  │  ← Price Bar (sticky)
└─────────────────────────────────┘
```

---

## Desktop Layout

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  ←  Back to Shop                 CUSTOMIZE YOUR [PRODUCT]                    │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌────────────────────────────────────────┐  ┌────────────────────────────┐ │
│  │                                        │  │  ZONE                      │ │
│  │                                        │  │  ┌──────┬──────┬──────┐    │ │
│  │           ┌──────────────┐             │  │  │FRONT │ BACK │ REAR │    │ │
│  │           │              │             │  │  │  ●   │      │      │    │ │
│  │           │              │             │  │  └──────┴──────┴──────┘    │ │
│  │           │   3D MODEL   │             │  │                            │ │
│  │           │              │             │  │  📷 ADD IMAGE              │ │
│  │           │   (rotate)   │             │  │  ┌────────────────────┐    │ │
│  │           │              │             │  │  │  ☁️ Drop image or  │    │ │
│  │           └──────────────┘             │  │  │     click to       │    │ │
│  │                                        │  │  │     browse         │    │ │
│  │         ↻ Drag to rotate               │  │  └────────────────────┘    │ │
│  │         🔍 Scroll to zoom              │  │                            │ │
│  │                                        │  │  ✏️ TEXT LAYERS            │ │
│  └────────────────────────────────────────┘  │  ┌────────────────────┐    │ │
│                                              │  │ Layer 1: "Hello"   │ ✕  │ │
│  VIEW ANGLES                                 │  ├────────────────────┤    │ │
│  ┌──────┬──────┬──────┬──────┐               │  │ + Add text layer   │    │ │
│  │Front │ Back │ Left │Right │               │  └────────────────────┘    │ │
│  └──────┴──────┴──────┴──────┘               │                            │ │
│                                              │  ────────────────────────  │ │
│                                              │  💰 TOTAL: $25.00          │ │
│                                              │  ┌──────────────────────┐  │ │
│                                              │  │   🛒 ADD TO CART     │  │ │
│                                              │  └──────────────────────┘  │ │
│                                              └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## 3D Preview Component

### Three.js Setup

```javascript
// assets/js/customizer/components/preview-3d.js

Alpine.data('preview3D', (config) => ({
  // State
  scene: null,
  camera: null,
  renderer: null,
  model: null,
  controls: null,
  isLoading: true,
  loadProgress: 0,

  // Config from product
  modelUrl: config.modelUrl,
  zones: config.zones,

  // Textures for each zone
  zoneTextures: {},

  init() {
    this.setupScene();
    this.loadModel();
    this.setupControls();
    this.animate();
  },

  setupScene() {
    // Scene
    this.scene = new THREE.Scene();
    this.scene.background = new THREE.Color(0x1a1a2e);

    // Camera
    this.camera = new THREE.PerspectiveCamera(45, this.getAspect(), 0.1, 1000);
    this.camera.position.set(0, 0, 5);

    // Renderer
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      alpha: true
    });
    this.renderer.setSize(this.getWidth(), this.getHeight());
    this.renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    this.$refs.canvas.appendChild(this.renderer.domElement);

    // Lighting
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
    this.scene.add(ambientLight);

    const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
    directionalLight.position.set(5, 5, 5);
    this.scene.add(directionalLight);
  },

  loadModel() {
    const loader = new THREE.GLTFLoader();

    loader.load(
      this.modelUrl,
      (gltf) => {
        this.model = gltf.scene;
        this.model.traverse((child) => {
          if (child.isMesh) {
            child.material = new THREE.MeshStandardMaterial({
              color: 0xffffff,
              roughness: 0.3,
              metalness: 0.1
            });
          }
        });
        this.scene.add(this.model);
        this.isLoading = false;
      },
      (progress) => {
        this.loadProgress = (progress.loaded / progress.total) * 100;
      },
      (error) => {
        console.error('Model load error:', error);
        this.$dispatch('model-error');
      }
    );
  },

  setupControls() {
    this.controls = new THREE.OrbitControls(this.camera, this.renderer.domElement);
    this.controls.enableDamping = true;
    this.controls.dampingFactor = 0.05;
    this.controls.enableZoom = true;
    this.controls.minDistance = 3;
    this.controls.maxDistance = 10;
    this.controls.enablePan = false;
  },

  animate() {
    requestAnimationFrame(() => this.animate());
    this.controls?.update();
    this.renderer?.render(this.scene, this.camera);
  },

  // Apply texture to zone
  applyTexture(zoneId, imageUrl) {
    const textureLoader = new THREE.TextureLoader();
    textureLoader.load(imageUrl, (texture) => {
      this.zoneTextures[zoneId] = texture;
      this.updateModelTexture();
    });
  },

  updateModelTexture() {
    // Implementation depends on model UV mapping
  },

  // Rotate to specific angle
  rotateTo(angle) {
    if (this.model) {
      gsap.to(this.model.rotation, {
        y: angle * (Math.PI / 180),
        duration: 0.5,
        ease: 'power2.out'
      });
    }
  },

  // View presets
  viewFront() { this.rotateTo(0); },
  viewBack() { this.rotateTo(180); },
  viewLeft() { this.rotateTo(-90); },
  viewRight() { this.rotateTo(90); },

  // Cleanup
  destroy() {
    this.renderer?.dispose();
    this.scene?.clear();
  }
}));
```

### 3D Preview HTML

```html
<div class="preview-3d-container"
     x-data="preview3D({
       modelUrl: '<?php echo $model_url; ?>',
       zones: <?php echo json_encode($zones); ?>
     })">

  <!-- Loading State -->
  <div class="preview-loading" x-show="isLoading">
    <div class="loading-spinner"></div>
    <div class="loading-progress">
      <div class="progress-bar" :style="{ width: loadProgress + '%' }"></div>
    </div>
    <span class="loading-text">Loading 3D model...</span>
  </div>

  <!-- 3D Canvas -->
  <div class="preview-canvas" x-ref="canvas" x-show="!isLoading"></div>

  <!-- Rotation Hint -->
  <div class="rotation-hint" x-show="!isLoading">
    <svg class="rotate-icon"><!-- rotate icon --></svg>
    <span>Drag to rotate</span>
  </div>

  <!-- View Angle Buttons (Desktop) -->
  <div class="view-angles hidden md:flex">
    <button @click="viewFront()" class="view-btn">Front</button>
    <button @click="viewBack()" class="view-btn">Back</button>
    <button @click="viewLeft()" class="view-btn">Left</button>
    <button @click="viewRight()" class="view-btn">Right</button>
  </div>

  <!-- Zoom Controls (Mobile) -->
  <div class="zoom-controls md:hidden">
    <button @click="zoomIn()" class="zoom-btn">+</button>
    <button @click="zoomOut()" class="zoom-btn">−</button>
  </div>
</div>
```

### 3D Preview CSS

```css
.preview-3d-container {
  position: relative;
  background: var(--surface-card);
  border-radius: 16px;
  overflow: hidden;
  aspect-ratio: 1;
}

@media (min-width: 768px) {
  .preview-3d-container {
    aspect-ratio: 4/3;
    min-height: 400px;
  }
}

.preview-canvas {
  width: 100%;
  height: 100%;
}

.preview-canvas canvas {
  width: 100% !important;
  height: 100% !important;
}

/* Loading State */
.preview-loading {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: var(--surface-card);
  gap: 16px;
}

.loading-spinner {
  width: 48px;
  height: 48px;
  border: 3px solid var(--border-subtle);
  border-top-color: var(--primary);
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.loading-progress {
  width: 200px;
  height: 4px;
  background: var(--surface-elevated);
  border-radius: 2px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background: var(--primary);
  transition: width 0.3s ease;
}

/* Rotation Hint */
.rotation-hint {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 20px;
  color: var(--text-secondary);
  font-size: 12px;
  pointer-events: none;
}

.rotate-icon {
  width: 16px;
  height: 16px;
  animation: rotate-hint 2s ease-in-out infinite;
}

@keyframes rotate-hint {
  0%, 100% { transform: rotate(-15deg); }
  50% { transform: rotate(15deg); }
}

/* View Angle Buttons */
.view-angles {
  position: absolute;
  bottom: 16px;
  left: 16px;
  display: flex;
  gap: 8px;
}

.view-btn {
  padding: 8px 12px;
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-primary);
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}

.view-btn:hover {
  background: var(--primary);
  border-color: var(--primary);
}

/* Zoom Controls (Mobile) */
.zoom-controls {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.zoom-btn {
  width: 40px;
  height: 40px;
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-primary);
  font-size: 20px;
  cursor: pointer;
}
```

---

## Zone Tabs Component

```html
<div class="zone-tabs" x-data="{ activeZone: 'front' }">
  <div class="tabs-container">
    <template x-for="zone in zones" :key="zone.id">
      <button class="zone-tab"
              :class="{ active: activeZone === zone.id }"
              @click="activeZone = zone.id; $dispatch('zone-change', zone.id)">
        <span class="zone-icon" x-html="zone.icon"></span>
        <span class="zone-label" x-text="zone.label"></span>
        <span class="zone-status" x-show="hasContent(zone.id)">●</span>
      </button>
    </template>
  </div>
</div>
```

```css
.zone-tabs {
  background: var(--surface-card);
  border-bottom: 1px solid var(--border-subtle);
  padding: 0 16px;
}

.tabs-container {
  display: flex;
  gap: 4px;
}

.zone-tab {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  padding: 12px 8px;
  background: transparent;
  border: none;
  color: var(--text-secondary);
  font-size: 12px;
  cursor: pointer;
  position: relative;
  transition: color 0.2s;
}

.zone-tab.active {
  color: var(--primary);
}

.zone-tab.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 20%;
  right: 20%;
  height: 3px;
  background: var(--primary);
  border-radius: 3px 3px 0 0;
}

.zone-icon {
  font-size: 20px;
}

.zone-status {
  position: absolute;
  top: 8px;
  right: 25%;
  color: var(--success);
  font-size: 8px;
}
```

---

## Image Upload Component

```html
<div class="upload-zone"
     x-data="imageUploader()"
     @dragover.prevent="isDragging = true"
     @dragleave="isDragging = false"
     @drop.prevent="handleDrop($event)"
     :class="{ 'dragging': isDragging, 'has-image': uploadedImage }">

  <!-- Empty State -->
  <div class="upload-empty" x-show="!uploadedImage">
    <input type="file"
           x-ref="fileInput"
           @change="handleFile($event)"
           accept="image/jpeg,image/png,application/pdf"
           hidden>

    <button class="upload-trigger" @click="$refs.fileInput.click()">
      <svg class="upload-icon"><!-- cloud upload --></svg>
      <span class="upload-title">Drag & drop or tap to browse</span>
      <span class="upload-hint">PNG, JPG, PDF up to 10MB</span>
    </button>
  </div>

  <!-- Image Preview -->
  <div class="upload-preview" x-show="uploadedImage">
    <img :src="uploadedImage" alt="Uploaded design">

    <!-- Image Controls -->
    <div class="image-controls">
      <button class="control-btn" @click="rotateImage()">
        <svg><!-- rotate icon --></svg>
      </button>
      <button class="control-btn" @click="flipImage()">
        <svg><!-- flip icon --></svg>
      </button>
      <button class="control-btn danger" @click="removeImage()">
        <svg><!-- trash icon --></svg>
      </button>
    </div>

    <!-- Scale Slider -->
    <div class="scale-control">
      <label>Scale</label>
      <input type="range" x-model="imageScale" min="50" max="150" step="5">
      <span x-text="imageScale + '%'"></span>
    </div>
  </div>

  <!-- Upload Progress -->
  <div class="upload-progress" x-show="isUploading">
    <div class="progress-bar" :style="{ width: uploadProgress + '%' }"></div>
    <span x-text="uploadProgress + '%'"></span>
  </div>
</div>
```

```css
.upload-zone {
  background: var(--surface-elevated);
  border: 2px dashed var(--border-subtle);
  border-radius: 12px;
  padding: 24px;
  text-align: center;
  transition: all 0.2s;
}

.upload-zone.dragging {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.upload-zone.has-image {
  border-style: solid;
  padding: 12px;
}

.upload-trigger {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  width: 100%;
  padding: 24px;
  background: transparent;
  border: none;
  cursor: pointer;
}

.upload-icon {
  width: 48px;
  height: 48px;
  color: var(--text-muted);
}

.upload-title {
  font-size: 14px;
  font-weight: 600;
  color: var(--text-primary);
}

.upload-hint {
  font-size: 12px;
  color: var(--text-muted);
}

/* Image Preview */
.upload-preview {
  position: relative;
}

.upload-preview img {
  width: 100%;
  max-height: 200px;
  object-fit: contain;
  border-radius: 8px;
}

.image-controls {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 12px;
}

.control-btn {
  width: 40px;
  height: 40px;
  background: var(--surface-card);
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-primary);
  cursor: pointer;
  transition: all 0.2s;
}

.control-btn:hover {
  background: var(--primary);
  border-color: var(--primary);
}

.control-btn.danger:hover {
  background: var(--error);
  border-color: var(--error);
}

.scale-control {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-top: 16px;
  padding: 12px;
  background: var(--surface-card);
  border-radius: 8px;
}

.scale-control label {
  font-size: 12px;
  color: var(--text-secondary);
}

.scale-control input[type="range"] {
  flex: 1;
}

.scale-control span {
  font-size: 12px;
  color: var(--text-primary);
  min-width: 40px;
}
```

---

## Text Layer Manager

```html
<div class="text-layers" x-data="textLayerManager()">
  <div class="layers-header">
    <span class="layers-title">✏️ Text Layers</span>
    <span class="layers-count" x-text="layers.length + '/3'"></span>
  </div>

  <!-- Layer List -->
  <div class="layers-list">
    <template x-for="(layer, index) in layers" :key="layer.id">
      <div class="layer-item" :class="{ active: activeLayer === layer.id }">
        <div class="layer-preview" @click="selectLayer(layer.id)">
          <span class="layer-text" x-text="layer.text || 'Empty'"></span>
        </div>

        <!-- Layer Controls (expanded when active) -->
        <div class="layer-controls" x-show="activeLayer === layer.id" x-collapse>
          <input type="text"
                 x-model="layer.text"
                 placeholder="Enter text..."
                 class="layer-input"
                 maxlength="30">

          <div class="layer-options">
            <!-- Font -->
            <select x-model="layer.font" class="layer-select">
              <option value="Arial">Arial</option>
              <option value="Roboto">Roboto</option>
              <option value="Pacifico">Script</option>
              <option value="Oswald">Bold</option>
            </select>

            <!-- Size -->
            <select x-model="layer.size" class="layer-select">
              <option value="12">Small</option>
              <option value="16">Medium</option>
              <option value="24">Large</option>
              <option value="32">X-Large</option>
            </select>

            <!-- Color -->
            <input type="color" x-model="layer.color" class="layer-color">
          </div>
        </div>

        <button class="layer-delete" @click="deleteLayer(layer.id)">
          <svg><!-- X icon --></svg>
        </button>
      </div>
    </template>
  </div>

  <!-- Add Layer Button -->
  <button class="add-layer-btn"
          @click="addLayer()"
          :disabled="layers.length >= 3">
    <svg><!-- plus icon --></svg>
    <span>Add text layer</span>
  </button>
</div>
```

```css
.text-layers {
  background: var(--surface-card);
  border-radius: 12px;
  padding: 16px;
}

.layers-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}

.layers-title {
  font-size: 14px;
  font-weight: 600;
  color: var(--text-primary);
}

.layers-count {
  font-size: 12px;
  color: var(--text-muted);
}

.layers-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.layer-item {
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  overflow: hidden;
  transition: all 0.2s;
}

.layer-item.active {
  border-color: var(--primary);
}

.layer-preview {
  display: flex;
  align-items: center;
  padding: 12px 16px;
  cursor: pointer;
}

.layer-text {
  flex: 1;
  font-size: 14px;
  color: var(--text-primary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.layer-controls {
  padding: 12px 16px;
  border-top: 1px solid var(--border-subtle);
  background: var(--surface-card);
}

.layer-input {
  width: 100%;
  padding: 10px 12px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  color: var(--text-primary);
  font-size: 14px;
  margin-bottom: 12px;
}

.layer-options {
  display: flex;
  gap: 8px;
}

.layer-select {
  flex: 1;
  padding: 8px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  color: var(--text-primary);
  font-size: 12px;
}

.layer-color {
  width: 40px;
  height: 36px;
  padding: 2px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  cursor: pointer;
}

.layer-delete {
  padding: 12px;
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  transition: color 0.2s;
}

.layer-delete:hover {
  color: var(--error);
}

.add-layer-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  width: 100%;
  padding: 12px;
  margin-top: 12px;
  background: transparent;
  border: 2px dashed var(--border-subtle);
  border-radius: 8px;
  color: var(--text-secondary);
  font-size: 14px;
  cursor: pointer;
  transition: all 0.2s;
}

.add-layer-btn:hover:not(:disabled) {
  border-color: var(--primary);
  color: var(--primary);
}

.add-layer-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

---

## Product-Specific Variations

### Mug (3-Zone)

```javascript
const mug3ZoneConfig = {
  modelUrl: '/assets/models/mug-standard.glb',
  zones: [
    { id: 'front', label: 'Front', width: 3.125, icon: '◐' },
    { id: 'back', label: 'Back', width: 3.125, icon: '◑' },
    { id: 'rear', label: 'Near Handle', width: 1.5, icon: '◧', textOnly: true }
  ],
  priceBase: 25,
  priceModifiers: [
    { trigger: 'has_image', amount: 5 },
    { trigger: 'text_layers > 1', amount: 2 }
  ]
};
```

### Mug (Full Wrap)

```javascript
const mugFullWrapConfig = {
  modelUrl: '/assets/models/mug-standard.glb',
  zones: [
    { id: 'wrap', label: 'Full Wrap', width: 7.75, height: 3.75, icon: '⭕' }
  ],
  priceBase: 30,
  features: {
    singleZone: true,
    seamlessWrap: true
  }
};
```

### Heart Handle Mug

```javascript
const mugHeartConfig = {
  modelUrl: '/assets/models/mug-heart.glb',
  zones: [
    { id: 'front', label: 'Front', icon: '◐' },
    { id: 'back', label: 'Back', icon: '◑' }
  ],
  options: {
    handleColor: {
      label: 'Handle Color',
      choices: [
        { id: 'red', hex: '#ff3366', label: 'Red' },
        { id: 'pink', hex: '#ff6b9d', label: 'Pink' },
        { id: 'white', hex: '#ffffff', label: 'White' }
      ]
    }
  },
  priceBase: 28
};
```

### Tumbler

```javascript
const tumblerConfig = {
  modelUrl: '/assets/models/tumbler.glb',
  zones: [
    { id: 'front', label: 'Front', icon: '◐' },
    { id: 'back', label: 'Back', icon: '◑' }
  ],
  options: {
    lidColor: {
      label: 'Lid Color',
      choices: [
        { id: 'black', hex: '#1a1a1a', label: 'Black' },
        { id: 'white', hex: '#ffffff', label: 'White' },
        { id: 'clear', hex: '#e0e0e0', label: 'Clear' }
      ]
    }
  },
  priceBase: 35
};
```

### Bottle

```javascript
const bottleConfig = {
  modelUrl: '/assets/models/bottle.glb',
  zones: [
    { id: 'front', label: 'Front', icon: '◐' },
    { id: 'back', label: 'Back', icon: '◑' }
  ],
  options: {
    bottleColor: {
      label: 'Bottle Color',
      choices: [
        { id: 'white', hex: '#ffffff', label: 'White' },
        { id: 'black', hex: '#1a1a1a', label: 'Black' },
        { id: 'silver', hex: '#c0c0c0', label: 'Silver' },
        { id: 'blue', hex: '#2563eb', label: 'Blue' }
      ]
    }
  },
  priceBase: 30
};
```

---

## Complete Alpine.js Component

```javascript
// assets/js/customizer/customizers/merchandise.js

Alpine.data('merchandiseCustomizer', (productConfig) => ({
  // Config
  config: productConfig,

  // State
  activeZone: productConfig.zones[0].id,
  zoneData: {},
  selectedOptions: {},
  isLoading: false,

  // Initialize zone data
  init() {
    this.config.zones.forEach(zone => {
      this.zoneData[zone.id] = {
        image: null,
        imageScale: 100,
        textLayers: []
      };
    });

    // Initialize options with defaults
    if (this.config.options) {
      Object.keys(this.config.options).forEach(key => {
        const opt = this.config.options[key];
        this.selectedOptions[key] = opt.choices[0].id;
      });
    }

    this.loadFromStorage();
  },

  // Computed
  get currentZone() {
    return this.zoneData[this.activeZone];
  },

  get totalPrice() {
    let price = this.config.priceBase;

    // Check all zones for content
    Object.values(this.zoneData).forEach(zone => {
      if (zone.image) {
        price += this.config.priceModifiers?.find(m => m.trigger === 'has_image')?.amount || 0;
      }
      if (zone.textLayers.length > 1) {
        price += (zone.textLayers.length - 1) * 2;
      }
    });

    return price;
  },

  get formattedPrice() {
    return '$' + this.totalPrice.toFixed(2);
  },

  get canAddToCart() {
    // At least one zone must have content
    return Object.values(this.zoneData).some(
      zone => zone.image || zone.textLayers.some(l => l.text.trim())
    );
  },

  // Methods
  setZone(zoneId) {
    this.activeZone = zoneId;
    this.$dispatch('zone-change', zoneId);
  },

  uploadImage(file) {
    // Validate
    if (!['image/jpeg', 'image/png', 'application/pdf'].includes(file.type)) {
      this.$dispatch('upload-error', 'Invalid file type');
      return;
    }
    if (file.size > 10 * 1024 * 1024) {
      this.$dispatch('upload-error', 'File too large (max 10MB)');
      return;
    }

    // Upload
    this.isLoading = true;
    const formData = new FormData();
    formData.append('file', file);
    formData.append('product_id', this.config.productId);
    formData.append('zone_id', this.activeZone);

    fetch('/wp-json/wpc/v1/upload', {
      method: 'POST',
      headers: { 'X-WP-Nonce': wpcData.nonce },
      body: formData
    })
    .then(res => res.json())
    .then(data => {
      this.currentZone.image = data.image.url;
      this.$dispatch('image-uploaded', { zone: this.activeZone, url: data.image.url });
      this.saveToStorage();
    })
    .catch(err => {
      this.$dispatch('upload-error', err.message);
    })
    .finally(() => {
      this.isLoading = false;
    });
  },

  removeImage() {
    this.currentZone.image = null;
    this.$dispatch('image-removed', this.activeZone);
    this.saveToStorage();
  },

  addTextLayer() {
    if (this.currentZone.textLayers.length >= 3) return;

    this.currentZone.textLayers.push({
      id: Date.now(),
      text: '',
      font: 'Arial',
      size: 16,
      color: '#ffffff'
    });
    this.saveToStorage();
  },

  deleteTextLayer(layerId) {
    this.currentZone.textLayers = this.currentZone.textLayers.filter(l => l.id !== layerId);
    this.saveToStorage();
  },

  setOption(key, value) {
    this.selectedOptions[key] = value;
    this.$dispatch('option-change', { key, value });
    this.saveToStorage();
  },

  saveToStorage() {
    const state = {
      zoneData: this.zoneData,
      selectedOptions: this.selectedOptions
    };
    localStorage.setItem(`wpc_${this.config.type}_${this.config.productId}`, JSON.stringify(state));
  },

  loadFromStorage() {
    const saved = localStorage.getItem(`wpc_${this.config.type}_${this.config.productId}`);
    if (saved) {
      const state = JSON.parse(saved);
      this.zoneData = { ...this.zoneData, ...state.zoneData };
      this.selectedOptions = { ...this.selectedOptions, ...state.selectedOptions };
    }
  },

  addToCart() {
    if (!this.canAddToCart) return;

    const designData = {
      product_id: this.config.productId,
      customizer_type: this.config.type,
      zones: this.zoneData,
      selected_options: this.selectedOptions,
      price: this.totalPrice
    };

    this.$dispatch('wpc-add-to-cart', designData);
  }
}));
```

---

## Accessibility Notes

- 3D preview has text alternative describing current view
- All controls keyboard accessible
- Touch targets 48x48px minimum
- Progress indicators have aria-live regions
- Color choices have text labels

---

## Performance Considerations

- Three.js lazy loaded when customizer becomes visible
- 3D models under 500KB each (GLB format)
- Image upload shows progress
- Texture updates debounced
- Model complexity: <10k triangles
