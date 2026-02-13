# Data Model: WooCommerce Product Customizer

**Feature**: 001-woo-product-customizer
**Date**: 2026-02-03

---

## Entity Overview

```
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│ WC_Product      │──1:N─│ ProductConfig   │──1:N─│ Zone            │
│ (WooCommerce)   │      │ (Plugin)        │      │                 │
└─────────────────┘      └─────────────────┘      └─────────────────┘
                                │
                                │ 1:N
                                ▼
                         ┌─────────────────┐
                         │ PriceModifier   │
                         └─────────────────┘

┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│ CustomerDesign  │──1:N─│ DesignZone      │──1:N─│ TextLayer       │
│                 │      │                 │      │                 │
└─────────────────┘      └─────────────────┘      └─────────────────┘
        │                        │
        │ 1:N                    │ 0:1
        ▼                        ▼
┌─────────────────┐      ┌─────────────────┐
│ DesignFile      │      │ UploadedImage   │
└─────────────────┘      └─────────────────┘
```

---

## Entities

### 1. ProductConfig

Product-level customizer configuration stored in `wp_postmeta`.

| Field | Type | Description | Storage |
|-------|------|-------------|---------|
| product_id | int | WooCommerce product ID | FK to wp_posts |
| customizer_enabled | bool | Whether customizer is active | `_wpc_enabled` |
| customizer_type | enum | Product type identifier | `_wpc_type` |
| zones | Zone[] | Available design zones | `_wpc_zones` (JSON) |
| price_modifiers | PriceModifier[] | Pricing rules | `_wpc_price_modifiers` (JSON) |
| options | object | Type-specific options | `_wpc_options` (JSON) |

**Customizer Types**:
```php
enum CustomizerType: string {
    case NEON = 'neon';
    case CARD = 'card';
    case MUG_3ZONE = 'mug_3zone';
    case MUG_FULLWRAP = 'mug_fullwrap';
    case MUG_HEART = 'mug_heart';
    case TUMBLER = 'tumbler';
    case BOTTLE = 'bottle';
    case TSHIRT = 'tshirt';
    case PEN = 'pen';
    case BAG = 'bag';
    case KEYCHAIN = 'keychain';
    case CAP = 'cap';
}
```

---

### 2. Zone

Design zone definition (where customers can add content).

| Field | Type | Description |
|-------|------|-------------|
| id | string | Unique zone identifier (e.g., "front", "back") |
| label | string | Display name (e.g., "Front Side") |
| width | float | Zone width in inches |
| height | float | Zone height in inches |
| allows_image | bool | Whether image upload is permitted |
| allows_text | bool | Whether text layers are permitted |
| max_text_layers | int | Maximum text layers (default: 3) |
| uv_mapping | object | 3D model UV coordinates (if applicable) |

**Example Zone Configuration (Mug 3-Zone)**:
```json
{
  "zones": [
    {
      "id": "front",
      "label": "Front",
      "width": 3.125,
      "height": 3.75,
      "allows_image": true,
      "allows_text": true,
      "max_text_layers": 3,
      "uv_mapping": { "u_start": 0.0, "u_end": 0.4, "v_start": 0.1, "v_end": 0.9 }
    },
    {
      "id": "back",
      "label": "Back",
      "width": 3.125,
      "height": 3.75,
      "allows_image": true,
      "allows_text": true,
      "max_text_layers": 3,
      "uv_mapping": { "u_start": 0.5, "u_end": 0.9, "v_start": 0.1, "v_end": 0.9 }
    },
    {
      "id": "rear",
      "label": "Near Handle",
      "width": 1.5,
      "height": 3.75,
      "allows_image": false,
      "allows_text": true,
      "max_text_layers": 1,
      "uv_mapping": { "u_start": 0.4, "u_end": 0.5, "v_start": 0.1, "v_end": 0.9 }
    }
  ]
}
```

---

### 3. PriceModifier

Dynamic pricing rules.

| Field | Type | Description |
|-------|------|-------------|
| id | string | Modifier identifier |
| type | enum | Modifier type (fixed, multiplier, tiered) |
| trigger | string | What triggers this modifier |
| value | float | Modifier value |
| label | string | Display label for cart |

**Modifier Types**:
```json
{
  "price_modifiers": [
    {
      "id": "size_large",
      "type": "multiplier",
      "trigger": "size=large",
      "value": 1.5,
      "label": "Large Size (+50%)"
    },
    {
      "id": "image_upload",
      "type": "fixed",
      "trigger": "has_image",
      "value": 5.00,
      "label": "Custom Image (+$5)"
    },
    {
      "id": "extra_text",
      "type": "fixed",
      "trigger": "text_layers>1",
      "value": 2.00,
      "label": "Additional Text (+$2 each)"
    },
    {
      "id": "quantity_500",
      "type": "multiplier",
      "trigger": "quantity>=500",
      "value": 0.90,
      "label": "Bulk Discount (-10%)"
    }
  ]
}
```

---

### 4. CustomerDesign

Customer's design state (stored in cart/session, then order meta).

| Field | Type | Description |
|-------|------|-------------|
| id | string | UUID for design |
| product_id | int | WooCommerce product ID |
| customizer_type | enum | Product type |
| zones | DesignZone[] | Content for each zone |
| selected_options | object | Type-specific selections |
| created_at | datetime | Creation timestamp |
| updated_at | datetime | Last update timestamp |

**Storage Locations**:
- Active design: `localStorage` (client) + `WC_Session` (server)
- Cart item: `$cart_item['wpc_design']`
- Order: `wp_woocommerce_order_itemmeta` with key `_wpc_design`

---

### 5. DesignZone

Content within a single zone.

| Field | Type | Description |
|-------|------|-------------|
| zone_id | string | Reference to Zone.id |
| image | UploadedImage | Uploaded image (optional) |
| text_layers | TextLayer[] | Text content layers |
| canvas_state | object | Fabric.js JSON state |

---

### 6. TextLayer

Individual text element.

| Field | Type | Description |
|-------|------|-------------|
| id | string | Layer identifier |
| content | string | Text content |
| font_family | string | Font name (e.g., "Roboto") |
| font_size | int | Size in pixels |
| color | string | Hex color (e.g., "#FF0000") |
| position_x | float | X position (0-1 normalized) |
| position_y | float | Y position (0-1 normalized) |
| rotation | float | Rotation in degrees |
| scale | float | Scale factor |

**Example**:
```json
{
  "id": "layer_1",
  "content": "Happy Birthday",
  "font_family": "Pacifico",
  "font_size": 48,
  "color": "#FF10F0",
  "position_x": 0.5,
  "position_y": 0.3,
  "rotation": 0,
  "scale": 1.0
}
```

---

### 7. UploadedImage

Customer-uploaded image file.

| Field | Type | Description |
|-------|------|-------------|
| id | string | UUID for image |
| original_name | string | Original filename |
| stored_path | string | Server path to file |
| url | string | Public URL |
| mime_type | string | MIME type |
| file_size | int | Size in bytes |
| dimensions | object | Width/height in pixels |
| uploaded_at | datetime | Upload timestamp |

**Storage Path Pattern**:
```
wp-content/uploads/wpc-designs/{year}/{month}/{design_id}/{image_id}.{ext}
```

---

### 8. DesignFile

Final design file for order fulfillment.

| Field | Type | Description |
|-------|------|-------------|
| id | string | UUID |
| order_id | int | WooCommerce order ID |
| order_item_id | int | Order line item ID |
| zone_id | string | Which zone this represents |
| file_path | string | Server path |
| file_type | string | 'preview' or 'print' |
| generated_at | datetime | Generation timestamp |

---

## Database Schema

### Custom Table: `{prefix}wpc_design_files`

```sql
CREATE TABLE {prefix}wpc_design_files (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    order_id BIGINT UNSIGNED NOT NULL,
    order_item_id BIGINT UNSIGNED NOT NULL,
    zone_id VARCHAR(50) NOT NULL,
    file_path VARCHAR(500) NOT NULL,
    file_type ENUM('preview', 'source', 'uploaded') NOT NULL,
    file_size BIGINT UNSIGNED DEFAULT 0,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_order (order_id),
    INDEX idx_order_item (order_item_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### Existing Tables Used

| Table | Usage |
|-------|-------|
| `wp_posts` | Product storage (post_type = 'product') |
| `wp_postmeta` | ProductConfig storage |
| `wp_woocommerce_sessions` | Active design session data |
| `wp_woocommerce_order_items` | Order line items |
| `wp_woocommerce_order_itemmeta` | CustomerDesign storage per order item |

---

## State Transitions

### Design Lifecycle

```
[Empty] → [Draft] → [Complete] → [In Cart] → [Ordered] → [Archived]
   │         │          │            │           │
   │         │          │            │           └─ Files retained 90 days
   │         │          │            └─ Validated, attached to order
   │         │          └─ Ready for cart (has content)
   │         └─ Has unsaved changes
   └─ No content yet
```

### Validation Rules

| State Transition | Validation |
|-----------------|------------|
| Draft → Complete | At least one zone has content |
| Complete → In Cart | All uploads successful, price calculated |
| In Cart → Ordered | Payment complete, files stored permanently |

---

## Type-Specific Options

### Neon Sign Options
```json
{
  "selected_options": {
    "text": "Happy Birthday",
    "color": "#ff10f0",
    "font": "Pacifico",
    "size": "medium",
    "background": "brick",
    "glow_intensity": 0.8
  }
}
```

### Visiting Card Options
```json
{
  "selected_options": {
    "template_id": "modern-01",
    "paper_finish": "gloss",
    "corner_style": "rounded",
    "quantity": 500,
    "fields": {
      "name": "John Doe",
      "title": "CEO",
      "phone": "+1 234 567 890",
      "email": "john@example.com",
      "address": "123 Main St"
    }
  }
}
```

### T-Shirt Options
```json
{
  "selected_options": {
    "color": "black",
    "size": "XL"
  }
}
```

---

## Indexes and Performance

| Query Pattern | Index |
|--------------|-------|
| Get product config | `wp_postmeta.meta_key` (existing) |
| Get order designs | `wpc_design_files.order_id` |
| Get item designs | `wpc_design_files.order_item_id` |
| Clean old files | `wpc_design_files.created_at` |
