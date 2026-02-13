# T-Shirt Customizer - UI/UX Design

**Product**: T-Shirt
**Style**: Bold & Colorful
**Priority**: Mobile-First
**Date**: 2026-02-03

---

## Overview

A multi-zone t-shirt designer with front/back/sleeve customization, color variants, size selection, and real-time flat preview with mockup visualization.

---

## Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Design Your T-Shirt          │
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │      ┌───────────┐        │  │
│  │      │           │        │  │
│  │   ┌──┤  DESIGN   ├──┐     │  │  ← T-Shirt Preview
│  │   │  │   AREA    │  │     │  │
│  │   │  │           │  │     │  │
│  │   │  └───────────┘  │     │  │
│  │   │                 │     │  │
│  │   │                 │     │  │
│  │   └─────────────────┘     │  │
│  │                           │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  SHIRT COLOR                    │
│  ⬤  ⬤  ⬤  ⬤  ⬤  ⬤  ⬤       │
│  Black White Navy Red ...       │
├─────────────────────────────────┤
│  ┌────────┬────────┬────────┐   │  ← Zone Tabs
│  │ FRONT  │  BACK  │ SLEEVES│   │
│  │   ●    │        │        │   │
│  └────────┴────────┴────────┘   │
├─────────────────────────────────┤
│                                 │
│  📷 ADD IMAGE                   │
│  ┌───────────────────────────┐  │
│  │  ☁️ Drag & drop or tap    │  │
│  │     PNG, JPG (max 10MB)   │  │
│  └───────────────────────────┘  │
│                                 │
│  ✏️ ADD TEXT                    │
│  ┌───────────────────────────┐  │
│  │ + Add text layer          │  │
│  └───────────────────────────┘  │
│                                 │
├─────────────────────────────────┤
│  📏 SELECT SIZE                 │
│  ┌────┬────┬────┬────┬────┬───┐│
│  │ XS │ S  │ M  │ L  │ XL │XXL││
│  │    │    │ ●  │    │    │   ││
│  └────┴────┴────┴────┴────┴───┘│
│                                 │
│  📐 Size Guide                  │
├─────────────────────────────────┤
│  💰 $29.00   [🛒 ADD TO CART]   │
└─────────────────────────────────┘
```

---

## Desktop Layout

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  ←  Back to Shop                  DESIGN YOUR T-SHIRT                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌────────────────────────────────────────┐  ┌────────────────────────────┐ │
│  │                                        │  │  👕 SHIRT COLOR            │ │
│  │        ┌─────────────────┐             │  │  ⬤ ⬤ ⬤ ⬤ ⬤ ⬤ ⬤ ⬤        │ │
│  │        │                 │             │  │  Black selected            │ │
│  │     ┌──┤   YOUR DESIGN   ├──┐          │  │                            │ │
│  │     │  │                 │  │          │  │  ZONE                      │ │
│  │     │  │                 │  │          │  │  ┌──────┬──────┬──────┐    │ │
│  │     │  │                 │  │          │  │  │FRONT │ BACK │SLEEVE│    │ │
│  │     │  └─────────────────┘  │          │  │  │  ●   │      │      │    │ │
│  │     │                       │          │  │  └──────┴──────┴──────┘    │ │
│  │     │                       │          │  │                            │ │
│  │     └───────────────────────┘          │  │  📷 ADD IMAGE              │ │
│  │                                        │  │  ┌────────────────────┐    │ │
│  │                                        │  │  │  ☁️ Drop or click  │    │ │
│  │                                        │  │  └────────────────────┘    │ │
│  └────────────────────────────────────────┘  │                            │ │
│                                              │  ✏️ TEXT LAYERS            │ │
│  VIEW: [Front] [Back] [Left] [Right]         │  ┌────────────────────┐    │ │
│                                              │  │ + Add text layer   │    │ │
│                                              │  └────────────────────┘    │ │
│                                              │                            │ │
│                                              │  📏 SIZE                   │ │
│                                              │  [XS][S][M][L][XL][XXL]    │ │
│                                              │        ●                   │ │
│                                              │                            │ │
│                                              │  ────────────────────────  │ │
│                                              │  💰 TOTAL: $29.00          │ │
│                                              │  ┌──────────────────────┐  │ │
│                                              │  │   🛒 ADD TO CART     │  │ │
│                                              │  └──────────────────────┘  │ │
│                                              └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## T-Shirt Preview Component

### SVG-Based Flat Preview

```html
<div class="tshirt-preview" :class="'color-' + shirtColor">
  <!-- T-Shirt SVG -->
  <svg viewBox="0 0 400 450" class="tshirt-svg">
    <!-- T-Shirt Shape -->
    <path class="tshirt-body" :fill="colorHex" d="
      M 85,50
      L 55,80
      L 25,130
      L 65,145
      L 80,100
      L 80,400
      L 320,400
      L 320,100
      L 335,145
      L 375,130
      L 345,80
      L 315,50
      L 260,50
      C 250,75 230,90 200,90
      C 170,90 150,75 140,50
      Z
    "/>

    <!-- Collar -->
    <path class="tshirt-collar" fill="none" stroke="#00000020" stroke-width="2" d="
      M 140,50
      C 150,75 170,90 200,90
      C 230,90 250,75 260,50
    "/>

    <!-- Design Area Indicator -->
    <rect class="design-area"
          x="110" y="120"
          width="180" height="200"
          fill="none"
          stroke="#ffffff40"
          stroke-dasharray="5,5"
          rx="4"/>

    <!-- User Design Container -->
    <foreignObject x="110" y="120" width="180" height="200" class="design-container">
      <div class="design-content">
        <!-- Image -->
        <img x-show="currentZone.image"
             :src="currentZone.image"
             :style="imageStyle"
             class="design-image">

        <!-- Text Layers -->
        <template x-for="layer in currentZone.textLayers">
          <div class="text-layer"
               :style="{
                 fontFamily: layer.font,
                 fontSize: layer.size + 'px',
                 color: layer.color,
                 transform: `translate(${layer.x}px, ${layer.y}px)`
               }"
               x-text="layer.text">
          </div>
        </template>
      </div>
    </foreignObject>
  </svg>

  <!-- Zone Label -->
  <div class="zone-label">
    <span x-text="activeZone.charAt(0).toUpperCase() + activeZone.slice(1)"></span> View
  </div>
</div>
```

### T-Shirt Preview CSS

```css
.tshirt-preview {
  position: relative;
  background: var(--surface-card);
  border-radius: 16px;
  padding: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tshirt-svg {
  width: 100%;
  max-width: 320px;
  height: auto;
}

.tshirt-body {
  transition: fill 0.3s ease;
}

/* Color variants */
.tshirt-preview.color-black .tshirt-body { fill: #1a1a1a; }
.tshirt-preview.color-white .tshirt-body { fill: #ffffff; stroke: #e0e0e0; stroke-width: 1; }
.tshirt-preview.color-navy .tshirt-body { fill: #1e3a5f; }
.tshirt-preview.color-red .tshirt-body { fill: #dc2626; }
.tshirt-preview.color-gray .tshirt-body { fill: #6b7280; }
.tshirt-preview.color-green .tshirt-body { fill: #059669; }
.tshirt-preview.color-blue .tshirt-body { fill: #2563eb; }
.tshirt-preview.color-yellow .tshirt-body { fill: #fbbf24; }

.design-area {
  pointer-events: none;
}

.design-container {
  overflow: hidden;
}

.design-content {
  width: 100%;
  height: 100%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.design-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  transition: transform 0.2s;
}

.text-layer {
  position: absolute;
  white-space: nowrap;
  text-align: center;
  pointer-events: none;
}

.zone-label {
  position: absolute;
  bottom: 12px;
  left: 50%;
  transform: translateX(-50%);
  padding: 6px 16px;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 20px;
  font-size: 12px;
  color: var(--text-primary);
}

/* Back view - flip the shirt */
.tshirt-preview.view-back .tshirt-svg {
  transform: scaleX(-1);
}

/* Sleeve view - show side angle */
.tshirt-preview.view-sleeve .tshirt-svg {
  transform: rotateY(45deg);
}
```

---

## Color Selector

```html
<div class="color-selector">
  <label class="selector-label">👕 Shirt Color</label>

  <div class="color-swatches">
    <template x-for="color in shirtColors" :key="color.id">
      <button class="color-swatch"
              :class="{ active: shirtColor === color.id }"
              :style="{ background: color.hex }"
              :title="color.name"
              @click="setColor(color.id)">
        <span class="color-check" x-show="shirtColor === color.id">✓</span>
      </button>
    </template>
  </div>

  <span class="color-name" x-text="selectedColorName"></span>
</div>
```

```css
.color-selector {
  padding: 16px 20px;
  background: var(--surface-card);
  border-radius: 12px;
}

.selector-label {
  display: block;
  font-size: 14px;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 12px;
}

.color-swatches {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.color-swatch {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  border: 2px solid transparent;
  cursor: pointer;
  position: relative;
  transition: all 0.2s;
}

.color-swatch:hover {
  transform: scale(1.1);
}

.color-swatch.active {
  border-color: var(--primary);
  box-shadow: 0 0 0 2px var(--surface-card), 0 0 0 4px var(--primary);
}

/* White swatch needs border */
.color-swatch[style*="#ffffff"],
.color-swatch[style*="#fff"] {
  border: 2px solid #e0e0e0;
}

.color-check {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  font-weight: bold;
}

/* Contrast check color based on background */
.color-swatch[style*="#1a1a1a"] .color-check,
.color-swatch[style*="#1e3a5f"] .color-check,
.color-swatch[style*="#dc2626"] .color-check,
.color-swatch[style*="#059669"] .color-check,
.color-swatch[style*="#2563eb"] .color-check {
  color: white;
}

.color-name {
  display: block;
  margin-top: 8px;
  font-size: 12px;
  color: var(--text-secondary);
  text-transform: capitalize;
}
```

---

## Size Selector with Guide

```html
<div class="size-selector">
  <div class="size-header">
    <label class="selector-label">📏 Select Size</label>
    <button class="size-guide-btn" @click="showSizeGuide = true">
      Size Guide
    </button>
  </div>

  <div class="size-buttons">
    <template x-for="size in sizes" :key="size">
      <button class="size-btn"
              :class="{ active: selectedSize === size }"
              @click="selectedSize = size">
        <span x-text="size"></span>
      </button>
    </template>
  </div>

  <!-- Size Guide Modal -->
  <div class="size-guide-modal"
       x-show="showSizeGuide"
       x-transition:enter="modal-enter"
       x-transition:leave="modal-leave"
       @click.self="showSizeGuide = false">
    <div class="modal-content">
      <div class="modal-header">
        <h3>Size Guide</h3>
        <button class="modal-close" @click="showSizeGuide = false">✕</button>
      </div>

      <table class="size-table">
        <thead>
          <tr>
            <th>Size</th>
            <th>Chest (in)</th>
            <th>Length (in)</th>
            <th>Sleeve (in)</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>XS</td><td>34-36</td><td>27</td><td>8</td></tr>
          <tr><td>S</td><td>36-38</td><td>28</td><td>8.5</td></tr>
          <tr><td>M</td><td>38-40</td><td>29</td><td>9</td></tr>
          <tr><td>L</td><td>40-42</td><td>30</td><td>9.5</td></tr>
          <tr><td>XL</td><td>42-44</td><td>31</td><td>10</td></tr>
          <tr><td>XXL</td><td>44-46</td><td>32</td><td>10.5</td></tr>
        </tbody>
      </table>

      <p class="size-tip">💡 Tip: Order one size up for a relaxed fit</p>
    </div>
  </div>
</div>
```

```css
.size-selector {
  background: var(--surface-card);
  border-radius: 12px;
  padding: 16px 20px;
}

.size-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}

.size-guide-btn {
  padding: 6px 12px;
  background: transparent;
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  color: var(--text-secondary);
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}

.size-guide-btn:hover {
  border-color: var(--primary);
  color: var(--primary);
}

.size-buttons {
  display: flex;
  gap: 8px;
}

.size-btn {
  flex: 1;
  padding: 14px 8px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-primary);
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.size-btn:hover {
  border-color: var(--text-muted);
}

.size-btn.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
  color: var(--primary);
}

/* Size Guide Modal */
.size-guide-modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  z-index: 1000;
}

.modal-content {
  background: var(--surface-card);
  border-radius: 16px;
  max-width: 500px;
  width: 100%;
  max-height: 80vh;
  overflow: auto;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid var(--border-subtle);
}

.modal-header h3 {
  font-size: 18px;
  font-weight: 600;
  color: var(--text-primary);
}

.modal-close {
  width: 32px;
  height: 32px;
  background: var(--surface-elevated);
  border: none;
  border-radius: 8px;
  color: var(--text-secondary);
  cursor: pointer;
}

.size-table {
  width: 100%;
  border-collapse: collapse;
}

.size-table th,
.size-table td {
  padding: 12px 16px;
  text-align: center;
  border-bottom: 1px solid var(--border-subtle);
}

.size-table th {
  background: var(--surface-elevated);
  font-size: 12px;
  font-weight: 600;
  color: var(--text-secondary);
  text-transform: uppercase;
}

.size-table td {
  font-size: 14px;
  color: var(--text-primary);
}

.size-tip {
  padding: 16px 20px;
  font-size: 13px;
  color: var(--text-secondary);
  background: var(--surface-elevated);
  border-radius: 0 0 16px 16px;
}
```

---

## Zone Configurations

```javascript
const tshirtConfig = {
  type: 'tshirt',
  zones: [
    {
      id: 'front',
      label: 'Front',
      icon: '👕',
      printArea: { x: 110, y: 120, width: 180, height: 200 },
      maxImageSize: { width: 12, height: 14 } // inches
    },
    {
      id: 'back',
      label: 'Back',
      icon: '🔙',
      printArea: { x: 110, y: 120, width: 180, height: 220 },
      maxImageSize: { width: 12, height: 16 }
    },
    {
      id: 'sleeve-left',
      label: 'Left Sleeve',
      icon: '💪',
      printArea: { x: 20, y: 100, width: 50, height: 80 },
      maxImageSize: { width: 3, height: 4 }
    },
    {
      id: 'sleeve-right',
      label: 'Right Sleeve',
      icon: '💪',
      printArea: { x: 330, y: 100, width: 50, height: 80 },
      maxImageSize: { width: 3, height: 4 }
    }
  ],
  colors: [
    { id: 'black', name: 'Black', hex: '#1a1a1a' },
    { id: 'white', name: 'White', hex: '#ffffff' },
    { id: 'navy', name: 'Navy Blue', hex: '#1e3a5f' },
    { id: 'red', name: 'Red', hex: '#dc2626' },
    { id: 'gray', name: 'Heather Gray', hex: '#6b7280' },
    { id: 'green', name: 'Forest Green', hex: '#059669' },
    { id: 'blue', name: 'Royal Blue', hex: '#2563eb' },
    { id: 'yellow', name: 'Yellow', hex: '#fbbf24' }
  ],
  sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL'],
  basePrice: 29,
  priceModifiers: [
    { trigger: 'has_back_design', amount: 5 },
    { trigger: 'has_sleeve_design', amount: 3 }
  ]
};
```

---

## Alpine.js Component

```javascript
Alpine.data('tshirtCustomizer', () => ({
  // State
  shirtColor: 'black',
  selectedSize: 'M',
  activeZone: 'front',
  showSizeGuide: false,
  zoneData: {},

  // Config
  shirtColors: [
    { id: 'black', name: 'Black', hex: '#1a1a1a' },
    { id: 'white', name: 'White', hex: '#ffffff' },
    { id: 'navy', name: 'Navy Blue', hex: '#1e3a5f' },
    { id: 'red', name: 'Red', hex: '#dc2626' },
    { id: 'gray', name: 'Heather Gray', hex: '#6b7280' },
    { id: 'green', name: 'Forest Green', hex: '#059669' },
    { id: 'blue', name: 'Royal Blue', hex: '#2563eb' },
    { id: 'yellow', name: 'Yellow', hex: '#fbbf24' }
  ],
  sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL'],
  zones: ['front', 'back', 'sleeve-left', 'sleeve-right'],

  init() {
    // Initialize zone data
    this.zones.forEach(zone => {
      this.zoneData[zone] = {
        image: null,
        imageScale: 100,
        textLayers: []
      };
    });
    this.loadFromStorage();
  },

  // Computed
  get currentZone() {
    return this.zoneData[this.activeZone];
  },

  get selectedColorName() {
    return this.shirtColors.find(c => c.id === this.shirtColor)?.name || '';
  },

  get colorHex() {
    return this.shirtColors.find(c => c.id === this.shirtColor)?.hex || '#1a1a1a';
  },

  get totalPrice() {
    let price = 29; // base price

    // Back design adds $5
    if (this.zoneData.back?.image || this.zoneData.back?.textLayers?.length) {
      price += 5;
    }

    // Sleeve designs add $3 each
    if (this.zoneData['sleeve-left']?.image || this.zoneData['sleeve-left']?.textLayers?.length) {
      price += 3;
    }
    if (this.zoneData['sleeve-right']?.image || this.zoneData['sleeve-right']?.textLayers?.length) {
      price += 3;
    }

    return price;
  },

  get formattedPrice() {
    return '$' + this.totalPrice.toFixed(2);
  },

  get canAddToCart() {
    return Object.values(this.zoneData).some(
      zone => zone.image || zone.textLayers?.some(l => l.text?.trim())
    );
  },

  // Methods
  setColor(colorId) {
    this.shirtColor = colorId;
    this.saveToStorage();
  },

  setZone(zoneId) {
    this.activeZone = zoneId;
  },

  uploadImage(file) {
    if (!file) return;

    const reader = new FileReader();
    reader.onload = (e) => {
      this.currentZone.image = e.target.result;
      this.saveToStorage();
    };
    reader.readAsDataURL(file);
  },

  removeImage() {
    this.currentZone.image = null;
    this.saveToStorage();
  },

  addTextLayer() {
    if (this.currentZone.textLayers.length >= 3) return;

    this.currentZone.textLayers.push({
      id: Date.now(),
      text: '',
      font: 'Arial',
      size: 24,
      color: this.shirtColor === 'white' ? '#000000' : '#ffffff',
      x: 50,
      y: 50
    });
    this.saveToStorage();
  },

  deleteTextLayer(layerId) {
    this.currentZone.textLayers = this.currentZone.textLayers.filter(l => l.id !== layerId);
    this.saveToStorage();
  },

  saveToStorage() {
    const state = {
      shirtColor: this.shirtColor,
      selectedSize: this.selectedSize,
      zoneData: this.zoneData
    };
    localStorage.setItem('wpc_tshirt_design', JSON.stringify(state));
  },

  loadFromStorage() {
    const saved = localStorage.getItem('wpc_tshirt_design');
    if (saved) {
      const state = JSON.parse(saved);
      this.shirtColor = state.shirtColor || 'black';
      this.selectedSize = state.selectedSize || 'M';
      if (state.zoneData) {
        this.zoneData = { ...this.zoneData, ...state.zoneData };
      }
    }
  },

  addToCart() {
    if (!this.canAddToCart) return;

    const designData = {
      product_id: this.$el.dataset.productId,
      customizer_type: 'tshirt',
      zones: this.zoneData,
      selected_options: {
        color: this.shirtColor,
        size: this.selectedSize
      },
      price: this.totalPrice
    };

    this.$dispatch('wpc-add-to-cart', designData);
  }
}));
```

---

## Design Tips Panel

```html
<div class="design-tips" x-data="{ expanded: false }">
  <button class="tips-toggle" @click="expanded = !expanded">
    <span>💡 Design Tips</span>
    <svg :class="{ 'rotate-180': expanded }"><!-- chevron --></svg>
  </button>

  <div class="tips-content" x-show="expanded" x-collapse>
    <ul class="tips-list">
      <li>
        <strong>Front:</strong> Best for logos and main graphics (up to 12" × 14")
      </li>
      <li>
        <strong>Back:</strong> Great for larger designs and text (up to 12" × 16")
      </li>
      <li>
        <strong>Sleeves:</strong> Perfect for small logos or numbers (up to 3" × 4")
      </li>
      <li>
        <strong>Colors:</strong> Use light designs on dark shirts, dark designs on light shirts
      </li>
      <li>
        <strong>Resolution:</strong> Upload images at 300 DPI for best print quality
      </li>
    </ul>
  </div>
</div>
```

```css
.design-tips {
  background: var(--surface-card);
  border-radius: 12px;
  overflow: hidden;
}

.tips-toggle {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 20px;
  background: transparent;
  border: none;
  color: var(--text-primary);
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
}

.tips-toggle svg {
  width: 20px;
  height: 20px;
  transition: transform 0.2s;
}

.tips-content {
  padding: 0 20px 20px;
}

.tips-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.tips-list li {
  padding: 8px 0;
  font-size: 13px;
  color: var(--text-secondary);
  border-bottom: 1px solid var(--border-subtle);
}

.tips-list li:last-child {
  border-bottom: none;
}

.tips-list strong {
  color: var(--text-primary);
}
```
