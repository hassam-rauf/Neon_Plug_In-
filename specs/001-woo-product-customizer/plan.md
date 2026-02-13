# Implementation Plan: WooCommerce Product Customizer Plugin

**Branch**: `001-woo-product-customizer` | **Date**: 2026-02-03 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-woo-product-customizer/spec.md`

---

## Summary

Build a WooCommerce plugin enabling customers to personalize 12 product types (Neon Signs, Visiting Cards, Mugs, T-Shirts, etc.) with real-time 3D/2D preview, image upload, multi-layer text, and dynamic pricing. The plugin uses Alpine.js for reactive UI, Three.js for 3D rendering, and integrates seamlessly with WooCommerce cart/checkout flow.

---

## Technical Context

**Language/Version**: PHP 8.0+ (WordPress/WooCommerce), JavaScript ES6+ (Frontend)
**Primary Dependencies**:
- Backend: WooCommerce 8.0+, WordPress 6.0+
- Frontend: Alpine.js 3.x, Three.js r150+, Fabric.js 5.x (2D canvas manipulation)
**Storage**: WordPress database (wp_postmeta, custom tables), wp-content/uploads for design files
**Testing**: PHPUnit (backend), Jest + Testing Library (frontend), Cypress (E2E)
**Target Platform**: WordPress websites with WooCommerce, modern browsers (Chrome/Firefox/Safari/Edge last 2 versions)
**Project Type**: WordPress plugin (monolithic with modular architecture)
**Performance Goals**: Preview updates <500ms, page load <3s, 100 concurrent sessions
**Constraints**: 10MB max upload, WebGL fallback to 2D, mobile-first responsive
**Scale/Scope**: Single WordPress installation, 12 product types, unlimited products per type

---

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|-----------|--------|-------|
| Modularity | ✅ PASS | Each product type as separate customizer module |
| Test-First | ✅ PASS | Unit tests for pricing, integration tests for cart |
| Simplicity | ✅ PASS | No over-engineering; direct WooCommerce hooks |
| Observability | ✅ PASS | WordPress debug logging, error tracking |
| Security | ✅ PASS | Nonce verification, file type validation, sanitization |

---

## Project Structure

### Documentation (this feature)

```text
specs/001-woo-product-customizer/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output (API schemas)
└── tasks.md             # Phase 2 output (/sp.tasks command)
```

### Source Code (repository root)

```text
woo-product-customizer/
├── woo-product-customizer.php      # Main plugin file
├── includes/
│   ├── class-wpc-loader.php        # Hook loader
│   ├── class-wpc-activator.php     # Activation hooks
│   ├── class-wpc-deactivator.php   # Deactivation hooks
│   │
│   ├── admin/
│   │   ├── class-wpc-admin.php           # Admin controller
│   │   ├── class-wpc-product-meta.php    # Product meta box
│   │   ├── class-wpc-settings.php        # Plugin settings
│   │   └── class-wpc-order-display.php   # Order customization view
│   │
│   ├── frontend/
│   │   ├── class-wpc-frontend.php        # Frontend controller
│   │   ├── class-wpc-customizer-loader.php  # Loads correct customizer
│   │   └── class-wpc-cart-handler.php    # Cart integration
│   │
│   ├── customizers/
│   │   ├── class-wpc-base-customizer.php    # Abstract base
│   │   ├── class-wpc-neon-customizer.php    # Product type 1
│   │   ├── class-wpc-card-customizer.php    # Product type 2
│   │   ├── class-wpc-mug-customizer.php     # Product types 3-5
│   │   ├── class-wpc-tumbler-customizer.php # Product type 6
│   │   ├── class-wpc-bottle-customizer.php  # Product type 7
│   │   ├── class-wpc-tshirt-customizer.php  # Product type 8
│   │   ├── class-wpc-pen-customizer.php     # Product type 9
│   │   ├── class-wpc-bag-customizer.php     # Product type 10
│   │   ├── class-wpc-keychain-customizer.php # Product type 11
│   │   └── class-wpc-cap-customizer.php     # Product type 12
│   │
│   ├── models/
│   │   ├── class-wpc-design.php          # Design data model
│   │   ├── class-wpc-text-layer.php      # Text layer model
│   │   └── class-wpc-price-calculator.php # Pricing logic
│   │
│   └── api/
│       ├── class-wpc-rest-controller.php  # REST API base
│       ├── class-wpc-upload-endpoint.php  # File upload
│       ├── class-wpc-design-endpoint.php  # Save/load designs
│       └── class-wpc-price-endpoint.php   # Price calculation
│
├── assets/
│   ├── js/
│   │   ├── customizer/
│   │   │   ├── app.js                    # Alpine.js main app
│   │   │   ├── components/
│   │   │   │   ├── preview-2d.js         # 2D canvas preview
│   │   │   │   ├── preview-3d.js         # Three.js 3D preview
│   │   │   │   ├── text-editor.js        # Text layer controls
│   │   │   │   ├── image-uploader.js     # Upload component
│   │   │   │   ├── color-picker.js       # Color selection
│   │   │   │   └── price-display.js      # Real-time price
│   │   │   ├── customizers/
│   │   │   │   ├── neon.js               # Neon-specific logic
│   │   │   │   ├── card.js               # Card-specific logic
│   │   │   │   ├── mug.js                # Mug-specific logic
│   │   │   │   └── ... (other types)
│   │   │   └── utils/
│   │   │       ├── canvas-helpers.js     # Fabric.js utilities
│   │   │       ├── three-helpers.js      # Three.js utilities
│   │   │       └── storage.js            # LocalStorage auto-save
│   │   └── admin/
│   │       └── product-meta.js           # Admin UI scripts
│   │
│   ├── css/
│   │   ├── customizer.css                # Main customizer styles
│   │   ├── responsive.css                # Mobile styles
│   │   └── admin.css                     # Admin panel styles
│   │
│   └── models/                           # 3D model files
│       ├── mug-standard.glb
│       ├── mug-heart-handle.glb
│       ├── tumbler.glb
│       ├── bottle.glb
│       └── tshirt.glb
│
├── templates/
│   ├── customizer/
│   │   ├── main.php                      # Main customizer template
│   │   ├── partials/
│   │   │   ├── preview-area.php          # Preview section
│   │   │   ├── controls-panel.php        # Controls section
│   │   │   ├── zone-tabs.php             # Zone navigation
│   │   │   └── layer-panel.php           # Layer management
│   │   └── product-types/
│   │       ├── neon.php                  # Neon-specific controls
│   │       ├── card.php                  # Card-specific controls
│   │       └── ... (other types)
│   │
│   ├── cart/
│   │   └── customization-details.php     # Cart item display
│   │
│   └── emails/
│       └── customization-details.php     # Email template
│
├── languages/
│   └── woo-product-customizer.pot        # Translation template
│
└── tests/
    ├── phpunit/
    │   ├── bootstrap.php
    │   ├── unit/
    │   │   ├── test-price-calculator.php
    │   │   ├── test-design-model.php
    │   │   └── test-file-validation.php
    │   └── integration/
    │       ├── test-cart-integration.php
    │       ├── test-order-storage.php
    │       └── test-rest-api.php
    │
    └── js/
        ├── jest.config.js
        ├── unit/
        │   ├── canvas-helpers.test.js
        │   └── price-display.test.js
        └── e2e/
            └── customizer-flow.cy.js
```

**Structure Decision**: WordPress plugin structure following WooCommerce extension patterns. Modular customizers allow adding new product types without modifying core code.

---

## Architecture Overview

### Component Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                        WooCommerce Product Page                      │
├─────────────────────────────────────────────────────────────────────┤
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                    Customizer Container                       │   │
│  │  ┌─────────────────────┐  ┌────────────────────────────────┐ │   │
│  │  │   Preview Panel     │  │      Controls Panel            │ │   │
│  │  │  ┌───────────────┐  │  │  ┌──────────────────────────┐  │ │   │
│  │  │  │ 3D Preview    │  │  │  │ Zone Tabs (Front/Back)   │  │ │   │
│  │  │  │ (Three.js)    │  │  │  └──────────────────────────┘  │ │   │
│  │  │  └───────────────┘  │  │  ┌──────────────────────────┐  │ │   │
│  │  │  ┌───────────────┐  │  │  │ Image Upload             │  │ │   │
│  │  │  │ 2D Fallback   │  │  │  │ (Drag & Drop)            │  │ │   │
│  │  │  │ (Fabric.js)   │  │  │  └──────────────────────────┘  │ │   │
│  │  │  └───────────────┘  │  │  ┌──────────────────────────┐  │ │   │
│  │  └─────────────────────┘  │  │ Text Layers              │  │ │   │
│  │                           │  │ (Add/Edit/Style)         │  │ │   │
│  │  ┌─────────────────────┐  │  └──────────────────────────┘  │ │   │
│  │  │   Price Display     │  │  ┌──────────────────────────┐  │ │   │
│  │  │   (Real-time)       │  │  │ Options (Color/Size/etc) │  │ │   │
│  │  └─────────────────────┘  │  └──────────────────────────┘  │ │   │
│  │                           └────────────────────────────────┘ │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │                    Add to Cart Button                          │  │
│  └───────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘

                              │
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         REST API Layer                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                  │
│  │ /upload     │  │ /design     │  │ /price      │                  │
│  │ (files)     │  │ (save/load) │  │ (calculate) │                  │
│  └─────────────┘  └─────────────┘  └─────────────┘                  │
└─────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      WooCommerce Integration                         │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐     │
│  │ Cart Handler    │  │ Order Meta      │  │ Email Templates │     │
│  │ (add/display)   │  │ (store design)  │  │ (include design)│     │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘     │
└─────────────────────────────────────────────────────────────────────┘
```

### Data Flow

```
User Action → Alpine.js State → Preview Update (Canvas/3D)
                    │
                    ├─→ Auto-save to LocalStorage
                    │
                    └─→ Price Calculation → Display Update

Add to Cart:
Design State → REST API → Validate → Store Files → Add Cart Meta
                                                          │
                                                          ▼
                                                    WooCommerce Cart
                                                          │
                                                          ▼
                                                    Order Complete
                                                          │
                                                          ▼
                                              Design Files + Metadata
                                              stored in Order Meta
```

---

## Technology Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Frontend Framework | Alpine.js | Lightweight, WordPress-friendly, no build step required |
| 3D Rendering | Three.js | Industry standard, extensive model support, WebGL |
| 2D Canvas | Fabric.js | Rich canvas API, text/image manipulation, JSON export |
| State Management | Alpine.js stores | Simple, adequate for single-page customizer |
| File Storage | wp-content/uploads | Standard WordPress pattern, works with existing backup |
| REST API | WP REST API | Native WordPress, familiar patterns, authentication built-in |
| 3D Models | GLTF/GLB | Compact, web-optimized, Three.js native support |

---

## Complexity Tracking

> No Constitution violations requiring justification.

| Area | Complexity | Justification |
|------|------------|---------------|
| 12 Product Types | Moderate | Required by business; mitigated via base class pattern |
| 3D + 2D Rendering | Moderate | Core feature requirement; 2D fallback ensures accessibility |
| Multi-zone Customization | Low-Moderate | Clear abstraction via Zone model |

---

## Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| 3D performance on mobile | High | Lazy load 3D, 2D fallback default on low-end devices |
| Large file uploads | Medium | Client-side compression, chunked upload, progress UI |
| Browser compatibility | Medium | Feature detection, graceful degradation |
| Cart data loss | High | Auto-save to localStorage, session backup |
| Theme conflicts | Medium | Scoped CSS, minimal DOM manipulation |

---

## Phase 0 Deliverables

- [x] Technical context defined
- [x] research.md - Technology research and decisions
- [x] Dependency evaluation complete

## Phase 1 Deliverables

- [x] data-model.md - Entity definitions
- [x] contracts/ - REST API specifications (OpenAPI 3.0)
- [x] quickstart.md - Development setup guide
- [x] Agent context updated

---

## Next Steps

Run `/sp.tasks` to generate actionable implementation tasks from this plan.
