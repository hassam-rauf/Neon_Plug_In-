# Visiting Card Customizer - UI/UX Design

**Product**: Visiting Card / Business Card
**Style**: Bold & Colorful
**Priority**: Mobile-First
**Date**: 2026-02-03

---

## Overview

A professional business card designer with front/back editing, logo upload, contact fields, templates, and paper finish options. Designed for B2B customers who need to create professional cards quickly.

---

## Mobile Layout

```
┌─────────────────────────────────┐
│ ←  Design Your Business Card    │  ← Header
├─────────────────────────────────┤
│  ┌───────────────────────────┐  │
│  │  ┌─────────────────────┐  │  │
│  │  │                     │  │  │
│  │  │    JOHN DOE         │  │  │  ← Card Preview
│  │  │    CEO              │  │  │     (flip animation)
│  │  │    +1 234 567 890   │  │  │
│  │  │    john@company.com │  │  │
│  │  │              [LOGO] │  │  │
│  │  └─────────────────────┘  │  │
│  │                           │  │
│  │     ⟳ Tap to flip        │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  ┌────────────┬────────────┐    │  ← Side Toggle
│  │   FRONT    │    BACK    │    │
│  │     ●      │            │    │
│  └────────────┴────────────┘    │
├─────────────────────────────────┤
│  📝 CONTACT DETAILS             │
│  ┌───────────────────────────┐  │
│  │ Name                      │  │
│  │ ┌───────────────────────┐ │  │
│  │ │ John Doe              │ │  │
│  │ └───────────────────────┘ │  │
│  │                           │  │
│  │ Title                     │  │
│  │ ┌───────────────────────┐ │  │
│  │ │ Chief Executive Officer│ │  │
│  │ └───────────────────────┘ │  │
│  │                           │  │
│  │ Phone                     │  │
│  │ ┌───────────────────────┐ │  │
│  │ │ +1 234 567 890        │ │  │
│  │ └───────────────────────┘ │  │
│  │                           │  │
│  │ Email                     │  │
│  │ ┌───────────────────────┐ │  │
│  │ │ john@company.com      │ │  │
│  │ └───────────────────────┘ │  │
│  │                           │  │
│  │ Address (optional)        │  │
│  │ ┌───────────────────────┐ │  │
│  │ │ 123 Business Ave      │ │  │
│  │ └───────────────────────┘ │  │
│  └───────────────────────────┘  │
│                                 │
│  🖼️ LOGO                        │
│  ┌───────────────────────────┐  │
│  │  ☁️ Upload logo           │  │
│  │     PNG, JPG (max 5MB)    │  │
│  └───────────────────────────┘  │
│                                 │
│  Position: ○ TL ○ TR ● BR ○ BL │
│                                 │
├─────────────────────────────────┤
│  📋 TEMPLATE                    │
│  ┌─────┬─────┬─────┬─────┐     │
│  │     │     │     │     │     │
│  │ Min │ Pro │ Bold│ Clas│     │
│  │  ●  │     │     │     │     │
│  └─────┴─────┴─────┴─────┘     │
├─────────────────────────────────┤
│  🎨 FINISH OPTIONS              │
│                                 │
│  Paper Finish                   │
│  ○ Matte  ● Gloss  ○ Textured  │
│                                 │
│  Corners                        │
│  ● Square  ○ Rounded           │
├─────────────────────────────────┤
│  📦 QUANTITY                    │
│  ┌─────────────────────────────┐│
│  │ ○ 100   $15                 ││
│  │ ○ 250   $30                 ││
│  │ ● 500   $50  ★ Best Value   ││
│  │ ○ 1000  $85                 ││
│  └─────────────────────────────┘│
├─────────────────────────────────┤
│  💰 $50.00    [🛒 ADD TO CART]  │
└─────────────────────────────────┘
```

---

## Desktop Layout

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  ←  Back to Shop               DESIGN YOUR BUSINESS CARD                     │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌────────────────────────────────────────┐  ┌────────────────────────────┐ │
│  │                                        │  │  📝 CONTACT DETAILS        │ │
│  │    ┌─────────────────────────────┐     │  │                            │ │
│  │    │                             │     │  │  Name                      │ │
│  │    │       JOHN DOE              │     │  │  ┌──────────────────────┐  │ │
│  │    │       Chief Executive       │     │  │  │ John Doe             │  │ │
│  │    │                             │     │  │  └──────────────────────┘  │ │
│  │    │       +1 234 567 890        │     │  │                            │ │
│  │    │       john@company.com      │     │  │  Title                     │ │
│  │    │       123 Business Ave      │     │  │  ┌──────────────────────┐  │ │
│  │    │                    [LOGO]   │     │  │  │ CEO                  │  │ │
│  │    │                             │     │  │  └──────────────────────┘  │ │
│  │    └─────────────────────────────┘     │  │                            │ │
│  │                                        │  │  Phone    Email            │ │
│  │         ⟳ Click to flip               │  │  ┌──────┐  ┌──────────┐    │ │
│  │                                        │  │  │      │  │          │    │ │
│  └────────────────────────────────────────┘  │  └──────┘  └──────────┘    │ │
│                                              │                            │ │
│  ┌──────────────┬──────────────┐             │  🖼️ LOGO                   │ │
│  │    FRONT     │     BACK     │             │  ┌────────────────────┐    │ │
│  │      ●       │              │             │  │ ☁️ Upload logo     │    │ │
│  └──────────────┴──────────────┘             │  └────────────────────┘    │ │
│                                              │  Position: [TR ▼]          │ │
│  📋 TEMPLATES                                │                            │ │
│  ┌──────┬──────┬──────┬──────┐               │  📦 QUANTITY & FINISH      │ │
│  │ Mini │ Pro  │ Bold │Classic│              │  Qty: [500 ▼]              │ │
│  │  ●   │      │      │      │               │  Finish: [Gloss ▼]         │ │
│  └──────┴──────┴──────┴──────┘               │  Corners: ● Square ○ Round │ │
│                                              │                            │ │
│                                              │  ────────────────────────  │ │
│                                              │  💰 TOTAL: $50.00          │ │
│                                              │  ┌──────────────────────┐  │ │
│                                              │  │   🛒 ADD TO CART     │  │ │
│                                              │  └──────────────────────┘  │ │
│                                              └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Card Preview Component

### Flip Animation

```css
.card-preview-container {
  perspective: 1000px;
  padding: 24px;
}

.card-preview {
  position: relative;
  width: 100%;
  max-width: 350px;
  aspect-ratio: 3.5 / 2; /* Standard business card ratio */
  margin: 0 auto;
  transform-style: preserve-3d;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
}

.card-preview.flipped {
  transform: rotateY(180deg);
}

.card-face {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  border-radius: 8px;
  box-shadow:
    0 4px 6px rgba(0, 0, 0, 0.1),
    0 10px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.card-front {
  background: #ffffff;
}

.card-back {
  background: #ffffff;
  transform: rotateY(180deg);
}

/* Paper finish effects */
.card-face.finish-matte {
  background: linear-gradient(135deg, #f8f8f8 0%, #ffffff 100%);
}

.card-face.finish-gloss {
  background: linear-gradient(135deg, #ffffff 0%, #f0f0f0 50%, #ffffff 100%);
  box-shadow:
    0 4px 6px rgba(0, 0, 0, 0.1),
    0 10px 20px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
}

.card-face.finish-textured {
  background:
    url('/textures/paper-texture.png'),
    linear-gradient(135deg, #fafafa 0%, #ffffff 100%);
  background-size: 200px 200px, 100% 100%;
}

/* Rounded corners option */
.card-face.corners-rounded {
  border-radius: 12px;
}

/* Flip hint */
.flip-hint {
  position: absolute;
  bottom: -32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  color: var(--text-muted);
}

.flip-icon {
  animation: flip-hint 2s ease-in-out infinite;
}

@keyframes flip-hint {
  0%, 100% { transform: rotateY(0); }
  50% { transform: rotateY(180deg); }
}
```

### Card Content Layout

```html
<div class="card-content" :class="'template-' + template">
  <!-- Logo -->
  <div class="card-logo"
       :class="'position-' + logoPosition"
       x-show="logo">
    <img :src="logo" alt="Company logo">
  </div>

  <!-- Name -->
  <div class="card-name" x-text="fields.name || 'Your Name'"></div>

  <!-- Title -->
  <div class="card-title" x-text="fields.title || 'Your Title'"></div>

  <!-- Contact Info -->
  <div class="card-contact">
    <div class="contact-item" x-show="fields.phone">
      <svg class="contact-icon"><!-- phone --></svg>
      <span x-text="fields.phone"></span>
    </div>
    <div class="contact-item" x-show="fields.email">
      <svg class="contact-icon"><!-- email --></svg>
      <span x-text="fields.email"></span>
    </div>
    <div class="contact-item" x-show="fields.address">
      <svg class="contact-icon"><!-- location --></svg>
      <span x-text="fields.address"></span>
    </div>
  </div>
</div>
```

```css
.card-content {
  position: absolute;
  inset: 0;
  padding: 20px;
  display: flex;
  flex-direction: column;
}

/* Template: Minimal */
.template-minimal .card-name {
  font-size: 18px;
  font-weight: 700;
  color: #1a1a2e;
  margin-top: auto;
}

.template-minimal .card-title {
  font-size: 12px;
  color: #6b7280;
  margin-bottom: 12px;
}

.template-minimal .card-contact {
  font-size: 10px;
  color: #374151;
}

/* Template: Professional */
.template-professional {
  background: linear-gradient(to right, #1a1a2e 0%, #1a1a2e 40%, #ffffff 40%);
}

.template-professional .card-name {
  position: absolute;
  left: 20px;
  top: 50%;
  transform: translateY(-50%) rotate(-90deg);
  transform-origin: left center;
  font-size: 16px;
  font-weight: 700;
  color: #ffffff;
  white-space: nowrap;
}

.template-professional .card-contact {
  position: absolute;
  right: 20px;
  top: 20px;
}

/* Template: Bold */
.template-bold {
  background: var(--primary);
}

.template-bold .card-name {
  font-size: 24px;
  font-weight: 800;
  color: #ffffff;
  text-transform: uppercase;
}

.template-bold .card-contact {
  color: rgba(255, 255, 255, 0.9);
}

/* Template: Classic */
.template-classic {
  border: 2px solid #1a1a2e;
}

.template-classic .card-name {
  font-family: 'Georgia', serif;
  font-size: 20px;
  text-align: center;
  margin-top: 30px;
}

/* Logo positioning */
.card-logo {
  position: absolute;
  width: 60px;
  height: 60px;
}

.card-logo img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.card-logo.position-tl { top: 16px; left: 16px; }
.card-logo.position-tr { top: 16px; right: 16px; }
.card-logo.position-bl { bottom: 16px; left: 16px; }
.card-logo.position-br { bottom: 16px; right: 16px; }
```

---

## Contact Form

```html
<div class="contact-form">
  <h3 class="form-title">📝 Contact Details</h3>

  <div class="form-grid">
    <!-- Name (Required) -->
    <div class="form-group full">
      <label class="form-label">
        Name <span class="required">*</span>
      </label>
      <input type="text"
             x-model="fields.name"
             placeholder="John Doe"
             class="form-input"
             required>
    </div>

    <!-- Title -->
    <div class="form-group full">
      <label class="form-label">Title / Position</label>
      <input type="text"
             x-model="fields.title"
             placeholder="Chief Executive Officer"
             class="form-input">
    </div>

    <!-- Phone -->
    <div class="form-group">
      <label class="form-label">Phone</label>
      <input type="tel"
             x-model="fields.phone"
             placeholder="+1 234 567 890"
             class="form-input">
    </div>

    <!-- Email -->
    <div class="form-group">
      <label class="form-label">Email</label>
      <input type="email"
             x-model="fields.email"
             placeholder="john@company.com"
             class="form-input">
    </div>

    <!-- Website -->
    <div class="form-group">
      <label class="form-label">Website</label>
      <input type="url"
             x-model="fields.website"
             placeholder="www.company.com"
             class="form-input">
    </div>

    <!-- Address -->
    <div class="form-group full">
      <label class="form-label">Address</label>
      <textarea x-model="fields.address"
                placeholder="123 Business Ave, City, State 12345"
                class="form-textarea"
                rows="2"></textarea>
    </div>
  </div>
</div>
```

```css
.contact-form {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 20px;
}

.form-title {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 16px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

@media (max-width: 480px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group.full {
  grid-column: 1 / -1;
}

.form-label {
  font-size: 12px;
  font-weight: 500;
  color: var(--text-secondary);
}

.form-label .required {
  color: var(--error);
}

.form-input,
.form-textarea {
  padding: 12px 14px;
  background: var(--surface-elevated);
  border: 1px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-primary);
  font-size: 14px;
  transition: all 0.2s;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(255, 107, 53, 0.15);
}

.form-input::placeholder,
.form-textarea::placeholder {
  color: var(--text-muted);
}

.form-textarea {
  resize: vertical;
  min-height: 60px;
}
```

---

## Logo Upload with Position

```html
<div class="logo-section">
  <h3 class="section-title">🖼️ Company Logo</h3>

  <!-- Upload Zone -->
  <div class="logo-upload"
       x-data="logoUploader()"
       :class="{ 'has-logo': logo }">

    <template x-if="!logo">
      <label class="upload-label">
        <input type="file"
               @change="handleUpload($event)"
               accept="image/png,image/jpeg"
               hidden>
        <svg class="upload-icon"><!-- upload --></svg>
        <span>Upload logo</span>
        <span class="upload-hint">PNG or JPG, max 5MB</span>
      </label>
    </template>

    <template x-if="logo">
      <div class="logo-preview">
        <img :src="logo" alt="Logo preview">
        <button class="remove-logo" @click="removeLogo()">
          <svg><!-- X --></svg>
        </button>
      </div>
    </template>
  </div>

  <!-- Position Selector -->
  <div class="position-selector" x-show="logo">
    <span class="position-label">Position on card:</span>
    <div class="position-grid">
      <button class="position-btn"
              :class="{ active: logoPosition === 'tl' }"
              @click="logoPosition = 'tl'"
              title="Top Left">
        <div class="position-indicator tl"></div>
      </button>
      <button class="position-btn"
              :class="{ active: logoPosition === 'tr' }"
              @click="logoPosition = 'tr'"
              title="Top Right">
        <div class="position-indicator tr"></div>
      </button>
      <button class="position-btn"
              :class="{ active: logoPosition === 'bl' }"
              @click="logoPosition = 'bl'"
              title="Bottom Left">
        <div class="position-indicator bl"></div>
      </button>
      <button class="position-btn"
              :class="{ active: logoPosition === 'br' }"
              @click="logoPosition = 'br'"
              title="Bottom Right">
        <div class="position-indicator br"></div>
      </button>
    </div>
  </div>
</div>
```

```css
.logo-section {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 20px;
}

.section-title {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 16px;
}

.logo-upload {
  border: 2px dashed var(--border-subtle);
  border-radius: 12px;
  padding: 24px;
  text-align: center;
  transition: all 0.2s;
}

.logo-upload:hover {
  border-color: var(--primary);
}

.logo-upload.has-logo {
  border-style: solid;
  padding: 12px;
}

.upload-label {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.upload-icon {
  width: 32px;
  height: 32px;
  color: var(--text-muted);
}

.upload-hint {
  font-size: 11px;
  color: var(--text-muted);
}

.logo-preview {
  position: relative;
  display: inline-block;
}

.logo-preview img {
  max-width: 120px;
  max-height: 60px;
  object-fit: contain;
}

.remove-logo {
  position: absolute;
  top: -8px;
  right: -8px;
  width: 24px;
  height: 24px;
  background: var(--error);
  border: none;
  border-radius: 50%;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Position Selector */
.position-selector {
  margin-top: 16px;
  padding-top: 16px;
  border-top: 1px solid var(--border-subtle);
}

.position-label {
  display: block;
  font-size: 12px;
  color: var(--text-secondary);
  margin-bottom: 12px;
}

.position-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  max-width: 120px;
}

.position-btn {
  aspect-ratio: 3.5 / 2;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  transition: all 0.2s;
}

.position-btn.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.position-indicator {
  position: absolute;
  width: 8px;
  height: 8px;
  background: var(--primary);
  border-radius: 2px;
}

.position-indicator.tl { top: 4px; left: 4px; }
.position-indicator.tr { top: 4px; right: 4px; }
.position-indicator.bl { bottom: 4px; left: 4px; }
.position-indicator.br { bottom: 4px; right: 4px; }
```

---

## Template Gallery

```html
<div class="template-section">
  <h3 class="section-title">📋 Templates</h3>

  <div class="template-grid">
    <button class="template-card"
            :class="{ active: template === 'minimal' }"
            @click="template = 'minimal'">
      <div class="template-preview minimal">
        <div class="t-name">Name</div>
        <div class="t-contact">contact</div>
      </div>
      <span class="template-name">Minimal</span>
    </button>

    <button class="template-card"
            :class="{ active: template === 'professional' }"
            @click="template = 'professional'">
      <div class="template-preview professional">
        <div class="t-accent"></div>
        <div class="t-content"></div>
      </div>
      <span class="template-name">Professional</span>
    </button>

    <button class="template-card"
            :class="{ active: template === 'bold' }"
            @click="template = 'bold'">
      <div class="template-preview bold">
        <div class="t-name">NAME</div>
      </div>
      <span class="template-name">Bold</span>
    </button>

    <button class="template-card"
            :class="{ active: template === 'classic' }"
            @click="template = 'classic'">
      <div class="template-preview classic">
        <div class="t-border"></div>
      </div>
      <span class="template-name">Classic</span>
    </button>
  </div>
</div>
```

```css
.template-section {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 20px;
}

.template-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
}

@media (max-width: 480px) {
  .template-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

.template-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  padding: 8px;
  background: transparent;
  border: 2px solid var(--border-subtle);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
}

.template-card:hover {
  border-color: var(--text-muted);
}

.template-card.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.template-preview {
  width: 100%;
  aspect-ratio: 3.5 / 2;
  background: #ffffff;
  border-radius: 4px;
  position: relative;
  overflow: hidden;
}

.template-name {
  font-size: 11px;
  color: var(--text-secondary);
}

/* Mini template previews */
.template-preview.minimal .t-name {
  position: absolute;
  bottom: 8px;
  left: 8px;
  font-size: 6px;
  font-weight: bold;
  color: #1a1a2e;
}

.template-preview.professional {
  display: flex;
}

.template-preview.professional .t-accent {
  width: 40%;
  background: #1a1a2e;
}

.template-preview.bold {
  background: var(--primary);
}

.template-preview.bold .t-name {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 6px;
  font-weight: 800;
  color: white;
}

.template-preview.classic .t-border {
  position: absolute;
  inset: 4px;
  border: 1px solid #1a1a2e;
}
```

---

## Finish & Quantity Options

```html
<div class="options-section">
  <h3 class="section-title">🎨 Finish Options</h3>

  <!-- Paper Finish -->
  <div class="option-group">
    <label class="option-label">Paper Finish</label>
    <div class="option-buttons">
      <button class="option-btn"
              :class="{ active: finish === 'matte' }"
              @click="finish = 'matte'">
        <span class="option-icon">📄</span>
        <span>Matte</span>
      </button>
      <button class="option-btn"
              :class="{ active: finish === 'gloss' }"
              @click="finish = 'gloss'">
        <span class="option-icon">✨</span>
        <span>Gloss</span>
      </button>
      <button class="option-btn"
              :class="{ active: finish === 'textured' }"
              @click="finish = 'textured'">
        <span class="option-icon">📃</span>
        <span>Textured</span>
      </button>
    </div>
  </div>

  <!-- Corners -->
  <div class="option-group">
    <label class="option-label">Corners</label>
    <div class="option-buttons">
      <button class="option-btn"
              :class="{ active: corners === 'square' }"
              @click="corners = 'square'">
        <span class="corner-icon square"></span>
        <span>Square</span>
      </button>
      <button class="option-btn"
              :class="{ active: corners === 'rounded' }"
              @click="corners = 'rounded'">
        <span class="corner-icon rounded"></span>
        <span>Rounded</span>
      </button>
    </div>
  </div>

  <!-- Quantity -->
  <div class="option-group">
    <label class="option-label">Quantity</label>
    <div class="quantity-options">
      <template x-for="qty in quantities" :key="qty.count">
        <button class="quantity-option"
                :class="{ active: quantity === qty.count, 'best-value': qty.bestValue }"
                @click="quantity = qty.count">
          <span class="qty-count" x-text="qty.count"></span>
          <span class="qty-price" x-text="'$' + qty.price"></span>
          <span class="qty-badge" x-show="qty.bestValue">Best Value</span>
        </button>
      </template>
    </div>
  </div>
</div>
```

```css
.options-section {
  background: var(--surface-card);
  border-radius: 16px;
  padding: 20px;
}

.option-group {
  margin-bottom: 20px;
}

.option-group:last-child {
  margin-bottom: 0;
}

.option-label {
  display: block;
  font-size: 12px;
  font-weight: 500;
  color: var(--text-secondary);
  margin-bottom: 10px;
}

.option-buttons {
  display: flex;
  gap: 8px;
}

.option-btn {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  padding: 12px 8px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 8px;
  color: var(--text-secondary);
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}

.option-btn:hover {
  border-color: var(--text-muted);
}

.option-btn.active {
  border-color: var(--primary);
  color: var(--text-primary);
  background: rgba(255, 107, 53, 0.1);
}

.option-icon {
  font-size: 18px;
}

.corner-icon {
  width: 20px;
  height: 14px;
  background: var(--text-muted);
}

.corner-icon.square {
  border-radius: 0;
}

.corner-icon.rounded {
  border-radius: 4px;
}

/* Quantity Options */
.quantity-options {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 8px;
}

@media (min-width: 480px) {
  .quantity-options {
    grid-template-columns: repeat(4, 1fr);
  }
}

.quantity-option {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  padding: 16px 12px;
  background: var(--surface-elevated);
  border: 2px solid var(--border-subtle);
  border-radius: 10px;
  cursor: pointer;
  position: relative;
  transition: all 0.2s;
}

.quantity-option:hover {
  border-color: var(--text-muted);
}

.quantity-option.active {
  border-color: var(--primary);
  background: rgba(255, 107, 53, 0.1);
}

.quantity-option.best-value {
  border-color: var(--success);
}

.quantity-option.best-value.active {
  border-color: var(--primary);
}

.qty-count {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
}

.qty-price {
  font-size: 14px;
  font-weight: 600;
  color: var(--accent);
}

.qty-badge {
  position: absolute;
  top: -8px;
  right: -8px;
  padding: 2px 6px;
  background: var(--success);
  color: white;
  font-size: 9px;
  font-weight: 600;
  border-radius: 4px;
  white-space: nowrap;
}
```

---

## Alpine.js Component

```javascript
Alpine.data('cardCustomizer', () => ({
  // State
  side: 'front',
  isFlipped: false,
  template: 'minimal',
  finish: 'gloss',
  corners: 'square',
  quantity: 500,
  logo: null,
  logoPosition: 'br',

  // Contact fields
  fields: {
    name: '',
    title: '',
    phone: '',
    email: '',
    website: '',
    address: ''
  },

  // Pricing
  quantities: [
    { count: 100, price: 15 },
    { count: 250, price: 30 },
    { count: 500, price: 50, bestValue: true },
    { count: 1000, price: 85 }
  ],

  // Computed
  get currentPrice() {
    const qty = this.quantities.find(q => q.count === this.quantity);
    return qty ? qty.price : 50;
  },

  get formattedPrice() {
    return '$' + this.currentPrice.toFixed(2);
  },

  get canAddToCart() {
    return this.fields.name.trim().length > 0;
  },

  // Methods
  flipCard() {
    this.isFlipped = !this.isFlipped;
    this.side = this.isFlipped ? 'back' : 'front';
  },

  setSide(side) {
    this.side = side;
    this.isFlipped = side === 'back';
  },

  uploadLogo(event) {
    const file = event.target.files[0];
    if (!file) return;

    if (!['image/png', 'image/jpeg'].includes(file.type)) {
      alert('Please upload PNG or JPG file');
      return;
    }

    if (file.size > 5 * 1024 * 1024) {
      alert('File too large (max 5MB)');
      return;
    }

    const reader = new FileReader();
    reader.onload = (e) => {
      this.logo = e.target.result;
    };
    reader.readAsDataURL(file);
  },

  removeLogo() {
    this.logo = null;
  },

  addToCart() {
    if (!this.canAddToCart) return;

    const designData = {
      product_id: this.$el.dataset.productId,
      customizer_type: 'card',
      selected_options: {
        template: this.template,
        finish: this.finish,
        corners: this.corners,
        quantity: this.quantity,
        fields: this.fields,
        logo: this.logo,
        logoPosition: this.logoPosition
      },
      price: this.currentPrice
    };

    this.$dispatch('wpc-add-to-cart', designData);
  },

  init() {
    // Load saved state
    const saved = localStorage.getItem('wpc_card_design');
    if (saved) {
      const state = JSON.parse(saved);
      Object.assign(this, state);
    }

    // Watch for changes
    this.$watch('fields', () => this.saveState(), { deep: true });
  },

  saveState() {
    localStorage.setItem('wpc_card_design', JSON.stringify({
      template: this.template,
      finish: this.finish,
      corners: this.corners,
      quantity: this.quantity,
      fields: this.fields,
      logoPosition: this.logoPosition
    }));
  }
}));
```

---

## Back Side Design

The back of the card can feature:
- Full logo centered
- QR code (auto-generated from website/contact)
- Tagline or company description
- Social media handles

```html
<div class="card-back-content" x-show="side === 'back'">
  <!-- Option: Large Logo -->
  <div class="back-logo" x-show="backDesign === 'logo'">
    <img :src="logo" alt="Company logo" x-show="logo">
    <span class="back-placeholder" x-show="!logo">Upload logo for back</span>
  </div>

  <!-- Option: QR Code -->
  <div class="back-qr" x-show="backDesign === 'qr'">
    <div class="qr-code" x-ref="qrCode"></div>
    <span class="qr-label">Scan to connect</span>
  </div>

  <!-- Back design selector -->
  <div class="back-options">
    <button @click="backDesign = 'logo'" :class="{ active: backDesign === 'logo' }">Logo</button>
    <button @click="backDesign = 'qr'" :class="{ active: backDesign === 'qr' }">QR Code</button>
    <button @click="backDesign = 'blank'" :class="{ active: backDesign === 'blank' }">Blank</button>
  </div>
</div>
```
