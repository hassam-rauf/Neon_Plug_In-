# Research: WooCommerce Product Customizer Plugin

**Feature**: 001-woo-product-customizer
**Date**: 2026-02-03
**Status**: Complete

---

## Research Questions

### 1. Best Practices for Three.js in WordPress/WooCommerce

**Decision**: Use Three.js r150+ with lazy loading and GLTF/GLB models

**Rationale**:
- Three.js is the industry standard for web 3D rendering
- GLTF/GLB format is optimized for web delivery (compressed, fast loading)
- Lazy loading prevents blocking page render
- WebGL 2.0 provides better performance on modern browsers

**Alternatives Considered**:
| Alternative | Why Rejected |
|------------|--------------|
| Babylon.js | Heavier bundle size, less WordPress examples |
| PlayCanvas | Requires account/hosting, not self-contained |
| CSS 3D | Insufficient for realistic product rendering |

**Implementation Notes**:
- Load Three.js only when customizer is active
- Use `THREE.GLTFLoader` for model loading
- Implement loading progress indicator
- Fallback to 2D preview if WebGL unavailable

---

### 2. Best Practices for Alpine.js in WooCommerce

**Decision**: Use Alpine.js 3.x with inline directives and global stores

**Rationale**:
- Lightweight (~15KB), no build step required
- Reactive by default, perfect for real-time preview updates
- Works alongside existing jQuery (WooCommerce uses jQuery)
- Easy to learn, WordPress-friendly

**Alternatives Considered**:
| Alternative | Why Rejected |
|------------|--------------|
| Vue.js | Requires build step, heavier bundle |
| React | Overkill for single component, conflicts with WP |
| Vanilla JS | More code, manual reactivity implementation |

**Implementation Notes**:
- Initialize Alpine after DOM ready
- Use `x-data` for component state
- Use `Alpine.store()` for shared state (design, price)
- Avoid conflicts with WooCommerce jQuery via noConflict

---

### 3. Best Practices for Image Upload in WordPress

**Decision**: Use WordPress REST API with custom endpoint, client-side validation

**Rationale**:
- WordPress REST API provides authentication via nonces
- Consistent with WordPress ecosystem
- Built-in file handling and security

**Alternatives Considered**:
| Alternative | Why Rejected |
|------------|--------------|
| Direct PHP upload | Less secure, no nonce verification |
| Third-party services | External dependency, GDPR concerns |
| WordPress media library | Too complex for customer uploads |

**Implementation Notes**:
- Client-side validation: file type (JPEG/PNG/PDF), size (<10MB)
- Server-side validation: MIME type, dimensions
- Store in `wp-content/uploads/wpc-designs/{order_id}/`
- Generate unique filenames to prevent collisions
- Implement chunked upload for large files

---

### 4. Fabric.js for 2D Canvas Manipulation

**Decision**: Use Fabric.js 5.x for 2D preview and text editing

**Rationale**:
- Rich API for canvas manipulation (add/move/scale/rotate)
- Built-in text editing with font support
- JSON serialization for state persistence
- Active community, good documentation

**Alternatives Considered**:
| Alternative | Why Rejected |
|------------|--------------|
| Konva.js | Less feature-rich for text editing |
| Paper.js | Better for vector, not raster operations |
| Native Canvas API | Too low-level, significant development time |

**Implementation Notes**:
- Create Fabric canvas for each design zone
- Use `fabric.Image` for uploaded images
- Use `fabric.IText` for editable text layers
- Export canvas state as JSON for persistence
- Generate preview image on save

---

### 5. WooCommerce Cart Integration Patterns

**Decision**: Use WooCommerce cart item meta and session storage

**Rationale**:
- `woocommerce_add_cart_item_data` hook for adding custom data
- `woocommerce_get_item_data` hook for displaying in cart
- `woocommerce_checkout_create_order_line_item` for order storage
- Standard patterns, works with all themes

**Implementation Notes**:
```php
// Add design data to cart
add_filter('woocommerce_add_cart_item_data', function($cart_item_data, $product_id) {
    if (isset($_POST['wpc_design'])) {
        $cart_item_data['wpc_design'] = sanitize_design_data($_POST['wpc_design']);
        $cart_item_data['unique_key'] = md5(microtime().rand());
    }
    return $cart_item_data;
}, 10, 2);

// Display in cart
add_filter('woocommerce_get_item_data', function($item_data, $cart_item) {
    if (isset($cart_item['wpc_design'])) {
        $item_data[] = [
            'key' => 'Custom Design',
            'value' => render_design_summary($cart_item['wpc_design'])
        ];
    }
    return $item_data;
}, 10, 2);
```

---

### 6. Neon Text Effect Rendering

**Decision**: Use CSS text-shadow with multiple layers + canvas glow filter

**Rationale**:
- Pure CSS for preview performance
- Canvas filter for high-quality render
- No external dependencies

**Implementation Notes**:
```css
/* CSS Neon Effect */
.neon-text {
    color: #fff;
    text-shadow:
        0 0 5px var(--neon-color),
        0 0 10px var(--neon-color),
        0 0 20px var(--neon-color),
        0 0 40px var(--neon-color);
}
```

**Color Options**:
| Color | Hex | Glow |
|-------|-----|------|
| Pink | #ff10f0 | Hot pink neon |
| Blue | #00d4ff | Cyan/electric blue |
| Green | #39ff14 | Neon green |
| Red | #ff073a | Neon red |
| Yellow | #fff01f | Neon yellow |
| White | #ffffff | White glow |

---

### 7. 3D Model Requirements for Products

**Decision**: Create/acquire GLB models with UV mapping for texture application

**Models Required**:
| Product | Model File | UV Zones |
|---------|-----------|----------|
| Mug (Standard) | mug-standard.glb | Front, Back, Rear |
| Mug (Heart Handle) | mug-heart.glb | Front, Back |
| Tumbler | tumbler.glb | Front, Back |
| Bottle | bottle.glb | Front, Back |
| T-Shirt | tshirt.glb | Front, Back, Sleeve L, Sleeve R |

**Model Specifications**:
- Polygon count: <10,000 triangles per model
- Texture resolution: 1024x1024 minimum
- Format: GLTF 2.0 / GLB (binary)
- File size target: <500KB per model

**Implementation Notes**:
- UV islands clearly mapped to print zones
- Apply customer design as texture via Three.js
- Update texture in real-time as design changes

---

### 8. Mobile Touch Interaction Patterns

**Decision**: Use Hammer.js for touch gestures on 3D preview, native touch for canvas

**Rationale**:
- Hammer.js handles pinch-zoom, rotation gestures
- Native touch events for drag operations
- Consistent experience across devices

**Implementation Notes**:
- Pinch to zoom 3D model
- Swipe/drag to rotate 3D model
- Touch and hold to position elements on canvas
- Double-tap to edit text
- Gesture conflicts: disable browser zoom in customizer area

---

### 9. Price Calculation Architecture

**Decision**: Server-side calculation with client-side preview, validated on add-to-cart

**Rationale**:
- Server-side is authoritative (prevents manipulation)
- Client-side preview for UX responsiveness
- Re-validate on checkout for security

**Price Factors**:
| Factor | Type | Example |
|--------|------|---------|
| Base price | Fixed | Product base price |
| Size modifier | Multiplier | Large = 1.5x |
| Image upload | Fixed add | +$5 per image |
| Extra text layers | Fixed add | +$2 per layer after first |
| Quantity tiers | Discount | 500 cards = 10% off |

**Implementation Notes**:
- Store pricing rules in product meta
- REST endpoint: `POST /wp-json/wpc/v1/calculate-price`
- Return breakdown: `{ base, modifiers[], total }`

---

### 10. Auto-Save and State Persistence

**Decision**: LocalStorage with session fallback, server sync on significant actions

**Rationale**:
- LocalStorage persists across page refreshes
- Session storage as fallback (incognito mode)
- Server sync on image upload and add-to-cart

**Implementation Notes**:
```javascript
// Auto-save design state
const saveDesign = debounce(() => {
    const state = Alpine.store('design').serialize();
    localStorage.setItem(`wpc_design_${productId}`, JSON.stringify(state));
}, 1000);

// Restore on page load
const restoreDesign = () => {
    const saved = localStorage.getItem(`wpc_design_${productId}`);
    if (saved) {
        Alpine.store('design').restore(JSON.parse(saved));
    }
};
```

---

## Dependencies Evaluation

### Frontend Dependencies

| Package | Version | Size | Purpose | Decision |
|---------|---------|------|---------|----------|
| Alpine.js | 3.x | 15KB | Reactive UI | ✅ Include |
| Three.js | r150+ | 150KB | 3D rendering | ✅ Include (lazy load) |
| Fabric.js | 5.x | 300KB | 2D canvas | ✅ Include (lazy load) |
| Hammer.js | 2.x | 7KB | Touch gestures | ✅ Include |

**Total estimated bundle**: ~470KB (lazy loaded, not blocking)

### Backend Dependencies

| Package | Version | Purpose | Decision |
|---------|---------|---------|----------|
| WooCommerce | 8.0+ | E-commerce platform | ✅ Required |
| WordPress | 6.0+ | CMS platform | ✅ Required |

**No additional PHP packages required** - using native WordPress/WooCommerce APIs.

---

## Security Considerations

| Area | Risk | Mitigation |
|------|------|------------|
| File upload | Malicious files | MIME validation, extension whitelist, virus scan hook |
| User input | XSS | Sanitize all text input, escape output |
| Price manipulation | Fraud | Server-side price calculation, re-validate on checkout |
| CSRF | Unauthorized actions | WordPress nonces on all forms/AJAX |
| Data exposure | Privacy | Limit design access to order owner + admin |

---

## Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| Initial page load | <3s | Lighthouse, real user monitoring |
| Preview update | <500ms | Performance API timing |
| 3D model load | <2s | Resource timing |
| Image upload | <5s for 5MB | XHR progress events |
| Add to cart | <1s | Ajax response time |

---

## Summary

All technical decisions resolved. No remaining NEEDS CLARIFICATION items.

**Ready for Phase 1**: data-model.md, contracts/, quickstart.md
