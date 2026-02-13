# UI/UX Design Documentation

**Feature**: WooCommerce Product Customizer Plugin
**Style**: Bold & Colorful
**Approach**: Mobile-First
**Date**: 2026-02-03

---

## Design Files Index

| File | Products Covered | Key Features |
|------|-----------------|--------------|
| [design-system.md](./design-system.md) | All products | Color palette, typography, components |
| [neon-sign-customizer.md](./neon-sign-customizer.md) | Neon Sign | Glow effects, dark canvas, real-time preview |
| [merchandise-3d-customizer.md](./merchandise-3d-customizer.md) | Mug, Tumbler, Bottle | Unified 3D preview, zones, Three.js |
| [visiting-card-customizer.md](./visiting-card-customizer.md) | Visiting Card | Form fields, templates, flip preview |
| [tshirt-customizer.md](./tshirt-customizer.md) | T-Shirt | SVG preview, color variants, size guide |
| [simple-products-customizer.md](./simple-products-customizer.md) | Pen, Keychain, Bags, Cap | 2D preview, bulk pricing |

---

## Product Coverage Matrix

| Product | Design File | Preview Type | Zones | Special Features |
|---------|-------------|--------------|-------|------------------|
| 1. Neon Sign | neon-sign-customizer.md | CSS Glow | Single | Text input, glow slider, backgrounds |
| 2. Visiting Card | visiting-card-customizer.md | 2D Flip | Front/Back | Form fields, templates, paper finish |
| 3. Mug (3-Zone) | merchandise-3d-customizer.md | 3D | Front/Back/Rear | Image + text per zone |
| 4. Mug (Full Wrap) | merchandise-3d-customizer.md | 3D | Single | Continuous wrap image |
| 5. Heart Handle Mug | merchandise-3d-customizer.md | 3D | Front/Back | Handle color picker |
| 6. Tumbler | merchandise-3d-customizer.md | 3D | Front/Back | Lid color option |
| 7. Bottle | merchandise-3d-customizer.md | 3D | Front/Back | Bottle color variants |
| 8. T-Shirt | tshirt-customizer.md | SVG 2D | Front/Back/Sleeves | Color/size variants |
| 9. Pen | simple-products-customizer.md | SVG 2D | Barrel | Bulk pricing, print color |
| 10. Bags | simple-products-customizer.md | SVG 2D | Front/Back | Multiple bag types |
| 11. Keychain | simple-products-customizer.md | 2D Flip | Front/Back | Shapes, visualization only |
| 12. Cap | simple-products-customizer.md | SVG 2D | Front/Side/Back | Style variants |

---

## Design System Summary

### Brand Colors

| Role | Color | Hex |
|------|-------|-----|
| Primary | Vibrant Orange | `#FF6B35` |
| Secondary | Electric Purple | `#7C3AED` |
| Accent | Cyan | `#06B6D4` |
| Surface Dark | Near Black | `#0A0A0F` |
| Surface Card | Dark Blue | `#1A1A2E` |

### Neon Colors

| Color | Hex |
|-------|-----|
| Pink | `#FF6B9D` |
| Blue | `#00D4FF` |
| Green | `#39FF14` |
| Red | `#FF3366` |
| Yellow | `#FFFF00` |
| White | `#FFFFFF` |

### Typography

- **Display**: Pacifico, Monoton, Bungee, Sacramento (neon fonts)
- **UI**: System font stack (`system-ui, -apple-system, sans-serif`)

---

## Shared Patterns

### Preview Layouts

**Mobile (stacked)**:
```
┌─────────────────┐
│    PREVIEW      │ ← Sticky
├─────────────────┤
│    TABS         │ ← Sticky
├─────────────────┤
│    CONTROLS     │ ← Scrollable
├─────────────────┤
│ PRICE │ CTA BTN │ ← Fixed bottom
└─────────────────┘
```

**Desktop (side-by-side)**:
```
┌─────────────────┬─────────────┐
│                 │             │
│    PREVIEW      │  CONTROLS   │
│    (sticky)     │  (scroll)   │
│                 │             │
│                 ├─────────────┤
│                 │ PRICE + CTA │
└─────────────────┴─────────────┘
```

### Component Library

All customizers share these components:
- **Image Upload Zone** - Drag/drop with preview
- **Text Layer Manager** - Add/edit/style text
- **Color Swatches** - Product color selection
- **Price Bar** - Sticky price + Add to Cart
- **Zone Tabs** - Switch between design zones

---

## Implementation Notes

### Frontend Stack
- **Alpine.js 3.x** - Reactive state management
- **Three.js** - 3D preview (merchandise)
- **Fabric.js** - 2D canvas manipulation
- **CSS** - Neon glow effects, animations

### Key Files to Implement
```
assets/
├── css/
│   ├── design-system/
│   │   ├── variables.css
│   │   ├── typography.css
│   │   └── components.css
│   └── customizers/
│       ├── neon.css
│       ├── merchandise.css
│       ├── card.css
│       ├── tshirt.css
│       └── simple.css
│
└── js/
    └── customizer/
        ├── app.js
        ├── components/
        │   ├── preview-3d.js
        │   ├── preview-2d.js
        │   ├── image-uploader.js
        │   ├── text-layers.js
        │   └── color-picker.js
        └── customizers/
            ├── neon.js
            ├── merchandise.js
            ├── card.js
            ├── tshirt.js
            └── simple.js
```

---

## Accessibility Checklist

All customizers must meet:
- [x] Touch targets ≥ 48px on mobile
- [x] Keyboard navigation for all controls
- [x] Focus indicators visible
- [x] Color contrast 4.5:1 (except decorative neon)
- [x] Error messages announced to screen readers
- [x] Progress indicators have aria-live

---

## Next Steps

1. Run `/sp.tasks` to generate implementation tasks
2. Implement design system CSS variables first
3. Build shared components
4. Implement product-specific customizers
5. Integrate with WooCommerce hooks
