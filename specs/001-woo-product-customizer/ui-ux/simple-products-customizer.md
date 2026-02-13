# Simple Products Customizer - UI/UX Design

**Products**: Pen, Keychain, Bags, Cap
**Style**: Bold & Colorful
**Priority**: Mobile-First
**Date**: 2026-02-03

---

## Overview

Simplified customizers for products with limited print areas. Uses 2D preview (no 3D) with straightforward upload/text options. Same design system as other customizers for consistency.

---

## 1. Pen Customizer

### Product Configuration

```javascript
const penConfig = {
  type: 'pen',
  preview: '2d',
  zones: [
    {
      id: 'barrel',
      label: 'Barrel',
      width: 2.5, // inches
      height: 0.5,
      textOnly: false,
      maxChars: 30
    }
  ],
  colors: [
    { id: 'black', name: 'Black', hex: '#1a1a1a' },
    { id: 'blue', name: 'Blue', hex: '#2563eb' },
    { id: 'red', name: 'Red', hex: '#dc2626' },
    { id: 'silver', name: 'Silver', hex: '#9ca3af' },
    { id: 'gold', name: 'Gold', hex: '#d4a574' }
  ],
  basePrice: 5,
  bulkPricing: [
    { qty: 25, price: 4.50 },
    { qty: 50, price: 4.00 },
    { qty: 100, price: 3.50 },
    { qty: 250, price: 3.00 }
  ]
};
```

### Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Customize Your Pen           │
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │   ━━━━━━━━━━━━━━━━━━━━━   │  │  ← Pen Preview
│  │   │ Your Text Here   │   │  │
│  │   ━━━━━━━━━━━━━━━━━━━━━   │  │
│  │                           │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  🖊️ PEN COLOR                   │
│  ⬤  ⬤  ⬤  ⬤  ⬤              │
│  Black                          │
├─────────────────────────────────┤
│  ✏️ YOUR TEXT                   │
│  ┌───────────────────────────┐  │
│  │ Company Name              │  │
│  └───────────────────────────┘  │
│                          20/30  │
│                                 │
│  🔤 PRINT COLOR                 │
│  ○ White  ● Gold  ○ Silver     │
├─────────────────────────────────┤
│  📦 QUANTITY                    │
│  ┌──────┬──────┬──────┬──────┐ │
│  │  25  │  50  │ 100  │ 250  │ │
│  │$4.50 │$4.00 │$3.50 │$3.00 │ │
│  │      │  ●   │      │      │ │
│  └──────┴──────┴──────┴──────┘ │
├─────────────────────────────────┤
│  💰 $200 (50 × $4) [ADD TO CART]│
└─────────────────────────────────┘
```

### Pen Preview CSS

```css
.pen-preview {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 40px 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.pen-svg {
  width: 100%;
  max-width: 300px;
}

.pen-body {
  transition: fill 0.3s ease;
}

.pen-print-area {
  fill: transparent;
}

.pen-text {
  font-size: 8px;
  text-anchor: middle;
  dominant-baseline: middle;
  transition: fill 0.3s ease;
}

/* Print colors */
.pen-text.print-white { fill: #ffffff; }
.pen-text.print-gold { fill: #d4a574; }
.pen-text.print-silver { fill: #c0c0c0; }
```

### Pen SVG Template

```html
<svg viewBox="0 0 300 60" class="pen-svg">
  <!-- Pen Body -->
  <rect class="pen-body"
        :fill="penColorHex"
        x="20" y="20"
        width="240" height="20"
        rx="2"/>

  <!-- Pen Tip -->
  <polygon class="pen-tip"
           fill="#c0c0c0"
           points="260,25 280,30 260,35"/>

  <!-- Pen Cap -->
  <rect class="pen-cap"
        :fill="penColorHex"
        x="10" y="18"
        width="20" height="24"
        rx="2"/>

  <!-- Clip -->
  <rect class="pen-clip"
        fill="#c0c0c0"
        x="12" y="8"
        width="4" height="20"
        rx="1"/>

  <!-- Print Area Text -->
  <text class="pen-text"
        :class="'print-' + printColor"
        x="140" y="30"
        x-text="penText || 'Your Text Here'">
  </text>
</svg>
```

---

## 2. Keychain Customizer

**Note**: Visualization only (per requirements)

### Product Configuration

```javascript
const keychainConfig = {
  type: 'keychain',
  preview: '2d',
  visualizationOnly: true, // Special flag
  shapes: [
    { id: 'circle', label: 'Circle', icon: '⭕' },
    { id: 'rectangle', label: 'Rectangle', icon: '▭' },
    { id: 'heart', label: 'Heart', icon: '❤️' },
    { id: 'star', label: 'Star', icon: '⭐' },
    { id: 'custom', label: 'Custom Shape', icon: '✂️' }
  ],
  zones: [
    { id: 'front', label: 'Front' },
    { id: 'back', label: 'Back' }
  ],
  basePrice: 8,
  bulkPricing: [
    { qty: 10, price: 7 },
    { qty: 25, price: 6 },
    { qty: 50, price: 5 }
  ]
};
```

### Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Design Your Keychain         │
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │       ○────────○          │  │  ← Keychain ring
│  │       │        │          │  │
│  │    ┌──┴────────┴──┐       │  │
│  │    │              │       │  │  ← Keychain body
│  │    │   [IMAGE]    │       │  │
│  │    │              │       │  │
│  │    └──────────────┘       │  │
│  │                           │  │
│  │      ⟳ Tap to flip       │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  🔷 SHAPE                       │
│  ┌─────┬─────┬─────┬─────┐     │
│  │ ⭕  │ ▭   │ ❤️  │ ⭐  │     │
│  │  ●  │     │     │     │     │
│  └─────┴─────┴─────┴─────┘     │
├─────────────────────────────────┤
│  SIDE: [FRONT ●] [BACK]         │
├─────────────────────────────────┤
│  📷 UPLOAD IMAGE                │
│  ┌───────────────────────────┐  │
│  │  ☁️ Drag & drop           │  │
│  │  PNG, JPG (max 5MB)       │  │
│  └───────────────────────────┘  │
│                                 │
│  ⚠️ This is a preview only.    │
│  Final product may vary.        │
├─────────────────────────────────┤
│  📦 QUANTITY                    │
│  [10][$7] [25][$6] [50][$5]    │
├─────────────────────────────────┤
│  💰 $175 (25 × $7) [ADD TO CART]│
└─────────────────────────────────┘
```

### Keychain Preview CSS

```css
.keychain-preview {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 32px 20px;
  text-align: center;
}

.keychain-container {
  display: inline-block;
  perspective: 500px;
}

.keychain-flipper {
  position: relative;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.keychain-flipper.flipped {
  transform: rotateY(180deg);
}

/* Ring */
.keychain-ring {
  width: 30px;
  height: 30px;
  border: 3px solid #c0c0c0;
  border-radius: 50%;
  margin: 0 auto 10px;
  position: relative;
}

.keychain-ring::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 2px;
  height: 15px;
  background: #c0c0c0;
}

/* Shape variations */
.keychain-body {
  width: 100px;
  height: 100px;
  background: #ffffff;
  border: 2px solid #e0e0e0;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  margin: 0 auto;
}

.keychain-body.shape-circle {
  border-radius: 50%;
}

.keychain-body.shape-rectangle {
  border-radius: 8px;
  width: 120px;
  height: 80px;
}

.keychain-body.shape-heart {
  width: 100px;
  height: 90px;
  background: #ffffff;
  clip-path: path('M50,90 C20,60 0,30 25,10 C40,0 50,10 50,25 C50,10 60,0 75,10 C100,30 80,60 50,90 Z');
  border: none;
}

.keychain-body.shape-star {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
  border: none;
}

/* Design preview */
.keychain-design {
  width: 80%;
  height: 80%;
  object-fit: contain;
}

/* Visualization warning */
.preview-warning {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 16px;
  background: rgba(245, 158, 11, 0.1);
  border: 1px solid var(--warning);
  border-radius: 8px;
  margin-top: 16px;
  font-size: 12px;
  color: var(--warning);
}
```

### Shape Selector

```html
<div class="shape-selector">
  <label class="selector-label">🔷 Select Shape</label>

  <div class="shape-options">
    <template x-for="shape in shapes" :key="shape.id">
      <button class="shape-option"
              :class="{ active: selectedShape === shape.id }"
              @click="selectedShape = shape.id">
        <span class="shape-icon" x-text="shape.icon"></span>
        <span class="shape-label" x-text="shape.label"></span>
      </button>
    </template>
  </div>
</div>
```

```css
.shape-options {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 8px;
}

.shape-option {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  padding: 12px 8px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
}

.shape-option:hover {
  border-color: var(--text-muted);
}

.shape-option.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.shape-icon {
  font-size: 24px;
}

.shape-label {
  font-size: 10px;
  color: var(--text-secondary);
}
```

---

## 3. Bags Customizer

### Product Configuration

```javascript
const bagConfig = {
  type: 'bag',
  preview: '2d',
  bagTypes: [
    { id: 'tote', label: 'Tote Bag', basePrice: 15 },
    { id: 'drawstring', label: 'Drawstring', basePrice: 12 },
    { id: 'laptop', label: 'Laptop Bag', basePrice: 35 },
    { id: 'shopping', label: 'Shopping Bag', basePrice: 8 }
  ],
  zones: [
    { id: 'front', label: 'Front', width: 10, height: 12 },
    { id: 'back', label: 'Back', width: 10, height: 12 }
  ],
  colors: [
    { id: 'natural', name: 'Natural', hex: '#e8dcc4' },
    { id: 'black', name: 'Black', hex: '#1a1a1a' },
    { id: 'navy', name: 'Navy', hex: '#1e3a5f' },
    { id: 'red', name: 'Red', hex: '#dc2626' }
  ]
};
```

### Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Customize Your Bag           │
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │      ╔═══════════╗        │  │  ← Handles
│  │      ║           ║        │  │
│  │   ┌──╨───────────╨──┐     │  │
│  │   │                 │     │  │
│  │   │   [YOUR LOGO]   │     │  │  ← Bag Preview
│  │   │                 │     │  │
│  │   │                 │     │  │
│  │   └─────────────────┘     │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  👜 BAG TYPE                    │
│  ┌─────────────────────────────┐│
│  │ ○ Tote Bag        $15      ││
│  │ ● Drawstring      $12      ││
│  │ ○ Laptop Bag      $35      ││
│  │ ○ Shopping Bag    $8       ││
│  └─────────────────────────────┘│
├─────────────────────────────────┤
│  🎨 BAG COLOR                   │
│  ⬤  ⬤  ⬤  ⬤                   │
│  Natural                        │
├─────────────────────────────────┤
│  SIDE: [FRONT ●] [BACK]         │
├─────────────────────────────────┤
│  📷 ADD IMAGE                   │
│  ┌───────────────────────────┐  │
│  │  ☁️ Drop or click         │  │
│  └───────────────────────────┘  │
│                                 │
│  ✏️ ADD TEXT                    │
│  [+ Add text layer]             │
├─────────────────────────────────┤
│  💰 $12.00    [🛒 ADD TO CART]  │
└─────────────────────────────────┘
```

### Bag Type Selector

```html
<div class="bag-type-selector">
  <label class="selector-label">👜 Select Bag Type</label>

  <div class="bag-types">
    <template x-for="bag in bagTypes" :key="bag.id">
      <label class="bag-type-option" :class="{ active: bagType === bag.id }">
        <input type="radio" :value="bag.id" x-model="bagType" hidden>
        <div class="bag-preview-icon" :class="'icon-' + bag.id"></div>
        <div class="bag-info">
          <span class="bag-name" x-text="bag.label"></span>
          <span class="bag-price" x-text="'$' + bag.basePrice"></span>
        </div>
        <span class="bag-radio"></span>
      </label>
    </template>
  </div>
</div>
```

```css
.bag-types {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.bag-type-option {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s;
}

.bag-type-option:hover {
  border-color: var(--text-muted);
}

.bag-type-option.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.bag-preview-icon {
  width: 40px;
  height: 40px;
  background: var(--surface-card);
  border-radius: 8px;
  /* Add bag type icons as background images */
}

.bag-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.bag-name {
  font-size: 14px;
  font-weight: 500;
  color: var(--text-primary);
}

.bag-price {
  font-size: 14px;
  font-weight: 600;
  color: var(--accent);
}

.bag-radio {
  width: 20px;
  height: 20px;
  border: 2px solid var(--border-subtle);
  border-radius: 50%;
  position: relative;
}

.bag-type-option.active .bag-radio {
  border-color: var(--primary);
}

.bag-type-option.active .bag-radio::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 10px;
  height: 10px;
  background: var(--primary);
  border-radius: 50%;
}
```

### Bag SVG Templates

```html
<!-- Tote Bag -->
<svg viewBox="0 0 200 220" class="bag-svg tote">
  <!-- Handles -->
  <path class="bag-handle" d="M 60,10 Q 60,40 60,50" stroke-width="6"/>
  <path class="bag-handle" d="M 140,10 Q 140,40 140,50" stroke-width="6"/>

  <!-- Body -->
  <path class="bag-body" :fill="bagColorHex" d="
    M 30,50
    L 30,200
    L 170,200
    L 170,50
    Z
  "/>

  <!-- Print Area -->
  <rect class="print-area"
        x="50" y="70"
        width="100" height="110"
        fill="none"
        stroke="#00000020"
        stroke-dasharray="4"/>
</svg>

<!-- Drawstring Bag -->
<svg viewBox="0 0 200 240" class="bag-svg drawstring">
  <!-- Strings -->
  <path class="bag-string" d="M 50,30 L 100,50 L 150,30"/>
  <path class="bag-string" d="M 50,30 L 50,10"/>
  <path class="bag-string" d="M 150,30 L 150,10"/>

  <!-- Body -->
  <path class="bag-body" :fill="bagColorHex" d="
    M 30,50
    Q 30,60 40,60
    L 40,220
    L 160,220
    L 160,60
    Q 170,60 170,50
    Q 100,70 30,50
    Z
  "/>
</svg>
```

---

## 4. Cap Customizer

### Product Configuration

```javascript
const capConfig = {
  type: 'cap',
  preview: '2d',
  zones: [
    { id: 'front', label: 'Front Panel', width: 4, height: 2.5 },
    { id: 'side', label: 'Side (optional)', width: 2, height: 1.5 },
    { id: 'back', label: 'Back Strap', width: 3, height: 0.5, textOnly: true }
  ],
  styles: [
    { id: 'baseball', label: 'Baseball Cap' },
    { id: 'snapback', label: 'Snapback' },
    { id: 'trucker', label: 'Trucker' },
    { id: 'dad', label: 'Dad Hat' }
  ],
  colors: [
    { id: 'black', name: 'Black', hex: '#1a1a1a' },
    { id: 'white', name: 'White', hex: '#ffffff' },
    { id: 'navy', name: 'Navy', hex: '#1e3a5f' },
    { id: 'red', name: 'Red', hex: '#dc2626' },
    { id: 'gray', name: 'Gray', hex: '#6b7280' },
    { id: 'khaki', name: 'Khaki', hex: '#c4b897' }
  ],
  basePrice: 22
};
```

### Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Customize Your Cap           │
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │      ╭─────────────╮      │  │
│  │    ╭─┤             ├─╮    │  │  ← Cap Preview
│  │   ╱  │  [LOGO]     │  ╲   │  │     (Front view)
│  │  │   │             │   │  │  │
│  │  │   ╰─────────────╯   │  │  │
│  │  ╰─────────────────────╯  │  │
│  │                           │  │
│  │   VIEW: [Front][Side][Back]│  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  🧢 CAP STYLE                   │
│  ┌──────┬──────┬──────┬──────┐ │
│  │ Base │ Snap │ Truck│ Dad  │ │
│  │  ●   │      │      │      │ │
│  └──────┴──────┴──────┴──────┘ │
├─────────────────────────────────┤
│  🎨 CAP COLOR                   │
│  ⬤  ⬤  ⬤  ⬤  ⬤  ⬤           │
│  Black                          │
├─────────────────────────────────┤
│  ZONE: [FRONT ●] [SIDE] [BACK]  │
├─────────────────────────────────┤
│  📷 ADD LOGO/IMAGE              │
│  ┌───────────────────────────┐  │
│  │  ☁️ Drop or click         │  │
│  │  Best size: 4" × 2.5"     │  │
│  └───────────────────────────┘  │
│                                 │
│  ✏️ ADD TEXT                    │
│  [+ Add embroidery text]        │
├─────────────────────────────────┤
│  💰 $22.00   [🛒 ADD TO CART]   │
└─────────────────────────────────┘
```

### Cap Preview

```css
.cap-preview {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 32px 20px;
}

.cap-container {
  position: relative;
  width: 200px;
  height: 150px;
  margin: 0 auto;
}

/* Cap SVG */
.cap-svg {
  width: 100%;
  height: 100%;
}

.cap-crown {
  transition: fill 0.3s ease;
}

.cap-brim {
  fill: currentColor;
  opacity: 0.9;
}

.cap-button {
  fill: currentColor;
}

/* Print area on front panel */
.cap-print-area {
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.cap-print-area img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

/* View angles */
.cap-views {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 16px;
}

.view-btn {
  padding: 8px 16px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  color: var(--text-secondary);
  font-size: 12px;
  cursor: pointer;
}

.view-btn.active {
  background: var(--primary);
  border-color: var(--primary);
  color: white;
}
```

### Cap SVG Template (Front View)

```html
<svg viewBox="0 0 200 150" class="cap-svg">
  <!-- Crown -->
  <path class="cap-crown" :fill="capColorHex" d="
    M 20,80
    Q 20,30 100,20
    Q 180,30 180,80
    L 180,100
    Q 100,110 20,100
    Z
  "/>

  <!-- Front Panel (lighter shade) -->
  <path class="cap-panel" :fill="capColorHex" filter="brightness(1.1)" d="
    M 40,80
    Q 40,40 100,30
    Q 160,40 160,80
    Q 100,90 40,80
    Z
  "/>

  <!-- Button on top -->
  <circle class="cap-button" :fill="capColorHex" cx="100" cy="18" r="6"/>

  <!-- Brim -->
  <ellipse class="cap-brim" :fill="capColorHex" cx="100" cy="100" rx="90" ry="20"/>

  <!-- Print Area Guide -->
  <rect class="print-guide"
        x="50" y="45"
        width="100" height="35"
        fill="none"
        stroke="#ffffff30"
        stroke-dasharray="3"
        rx="2"/>
</svg>
```

---

## Shared Components

### Bulk Quantity Selector

Used by Pen, Keychain, and other bulk-order products.

```html
<div class="bulk-qty-selector">
  <label class="selector-label">📦 Quantity</label>

  <div class="qty-grid">
    <template x-for="tier in bulkPricing" :key="tier.qty">
      <button class="qty-option"
              :class="{
                active: quantity === tier.qty,
                'best-value': tier.qty === recommendedQty
              }"
              @click="quantity = tier.qty">
        <span class="qty-count" x-text="tier.qty"></span>
        <span class="qty-price" x-text="'$' + tier.price.toFixed(2) + '/ea'"></span>
        <span class="qty-badge" x-show="tier.qty === recommendedQty">Best Value</span>
      </button>
    </template>
  </div>

  <!-- Custom quantity input -->
  <div class="custom-qty">
    <label>
      <input type="checkbox" x-model="useCustomQty">
      Custom quantity
    </label>
    <input type="number"
           x-show="useCustomQty"
           x-model="customQty"
           min="1"
           placeholder="Enter qty">
  </div>

  <!-- Total -->
  <div class="qty-total">
    <span>Total: <span x-text="quantity"></span> items</span>
    <span class="total-price" x-text="'$' + totalPrice.toFixed(2)"></span>
  </div>
</div>
```

```css
.bulk-qty-selector {
  background: var(--surface-card);
  border-radius: 12px;
  padding: 16px 20px;
}

.qty-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 8px;
  margin-bottom: 16px;
}

@media (max-width: 400px) {
  .qty-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

.qty-option {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
  padding: 12px 8px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 8px;
  cursor: pointer;
  position: relative;
  transition: all 0.2s;
}

.qty-option:hover {
  border-color: var(--text-muted);
}

.qty-option.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.qty-option.best-value {
  border-color: var(--success);
}

.qty-count {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
}

.qty-price {
  font-size: 12px;
  color: var(--accent);
}

.qty-badge {
  position: absolute;
  top: -8px;
  right: -4px;
  padding: 2px 6px;
  background: var(--success);
  color: white;
  font-size: 8px;
  font-weight: 600;
  border-radius: 4px;
  white-space: nowrap;
}

.custom-qty {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 0;
  border-top: 1px solid var(--border-subtle);
}

.custom-qty label {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 13px;
  color: var(--text-secondary);
  cursor: pointer;
}

.custom-qty input[type="number"] {
  width: 100px;
  padding: 8px 12px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  color: var(--text-primary);
}

.qty-total {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 12px;
  border-top: 1px solid var(--border-subtle);
  font-size: 14px;
  color: var(--text-secondary);
}

.total-price {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
}
```

---

## Alpine.js Component (Generic Simple Product)

```javascript
Alpine.data('simpleCustomizer', (config) => ({
  // Config
  config: config,

  // State
  productColor: config.colors?.[0]?.id || 'black',
  quantity: config.bulkPricing?.[1]?.qty || 1,
  useCustomQty: false,
  customQty: 1,
  activeZone: config.zones?.[0]?.id || 'front',
  selectedStyle: config.styles?.[0]?.id || null,
  selectedBagType: config.bagTypes?.[0]?.id || null,
  selectedShape: config.shapes?.[0]?.id || null,
  printColor: 'white',
  text: '',
  zoneData: {},

  init() {
    // Initialize zone data
    if (this.config.zones) {
      this.config.zones.forEach(zone => {
        this.zoneData[zone.id] = {
          image: null,
          text: '',
          textLayers: []
        };
      });
    }
    this.loadFromStorage();
  },

  // Computed
  get currentZone() {
    return this.zoneData[this.activeZone] || {};
  },

  get effectiveQty() {
    return this.useCustomQty ? this.customQty : this.quantity;
  },

  get unitPrice() {
    if (this.config.bulkPricing) {
      // Find matching tier (highest qty that's <= selected)
      const tiers = [...this.config.bulkPricing].sort((a, b) => b.qty - a.qty);
      const tier = tiers.find(t => t.qty <= this.effectiveQty);
      return tier ? tier.price : this.config.basePrice;
    }

    // Bag type pricing
    if (this.config.bagTypes && this.selectedBagType) {
      const bag = this.config.bagTypes.find(b => b.id === this.selectedBagType);
      return bag ? bag.basePrice : this.config.basePrice;
    }

    return this.config.basePrice;
  },

  get totalPrice() {
    return this.unitPrice * this.effectiveQty;
  },

  get formattedPrice() {
    return '$' + this.totalPrice.toFixed(2);
  },

  get productColorHex() {
    const color = this.config.colors?.find(c => c.id === this.productColor);
    return color?.hex || '#1a1a1a';
  },

  get canAddToCart() {
    // Check if any zone has content
    return Object.values(this.zoneData).some(
      zone => zone.image || zone.text?.trim() || zone.textLayers?.some(l => l.text?.trim())
    );
  },

  // Methods
  setColor(colorId) {
    this.productColor = colorId;
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

  saveToStorage() {
    const state = {
      productColor: this.productColor,
      quantity: this.quantity,
      selectedStyle: this.selectedStyle,
      selectedBagType: this.selectedBagType,
      selectedShape: this.selectedShape,
      zoneData: this.zoneData
    };
    localStorage.setItem(`wpc_${this.config.type}_design`, JSON.stringify(state));
  },

  loadFromStorage() {
    const saved = localStorage.getItem(`wpc_${this.config.type}_design`);
    if (saved) {
      const state = JSON.parse(saved);
      Object.assign(this, state);
    }
  },

  addToCart() {
    if (!this.canAddToCart) return;

    const designData = {
      product_id: this.$el.dataset.productId,
      customizer_type: this.config.type,
      zones: this.zoneData,
      selected_options: {
        color: this.productColor,
        quantity: this.effectiveQty,
        style: this.selectedStyle,
        bagType: this.selectedBagType,
        shape: this.selectedShape,
        printColor: this.printColor
      },
      price: this.totalPrice
    };

    this.$dispatch('wpc-add-to-cart', designData);
  }
}));
```
