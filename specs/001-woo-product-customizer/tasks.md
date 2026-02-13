# Tasks: WooCommerce Product Customizer Plugin

**Input**: Design documents from `/specs/001-woo-product-customizer/`
**Prerequisites**: plan.md ✅, spec.md ✅, data-model.md ✅
**Branch**: `001-woo-product-customizer`

**Tests**: Not explicitly requested in specification. Test tasks omitted.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

Based on plan.md, this is a WordPress plugin with structure:
- `woo-product-customizer/` - Plugin root
- `includes/` - PHP classes
- `assets/js/` - JavaScript files
- `assets/css/` - Stylesheets
- `templates/` - PHP templates

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Plugin initialization and basic structure

- [ ] T001 Create plugin directory structure per plan.md in `woo-product-customizer/`
- [ ] T002 Create main plugin file with headers and hooks in `woo-product-customizer/woo-product-customizer.php`
- [ ] T003 [P] Create loader class for hook registration in `includes/class-wpc-loader.php`
- [ ] T004 [P] Create activator class with activation hooks in `includes/class-wpc-activator.php`
- [ ] T005 [P] Create deactivator class with cleanup hooks in `includes/class-wpc-deactivator.php`
- [ ] T006 [P] Setup composer.json for PHP dependencies in `woo-product-customizer/composer.json`
- [ ] T007 [P] Setup package.json for frontend dependencies in `woo-product-customizer/package.json`
- [ ] T008 Configure Alpine.js, Three.js, and Fabric.js CDN loading in `includes/frontend/class-wpc-frontend.php`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

### Database & Models

- [ ] T009 Create database migration for `wpc_design_files` table in `includes/class-wpc-activator.php`
- [ ] T010 [P] Create Design model class in `includes/models/class-wpc-design.php`
- [ ] T011 [P] Create TextLayer model class in `includes/models/class-wpc-text-layer.php`
- [ ] T012 [P] Create PriceCalculator class in `includes/models/class-wpc-price-calculator.php`

### REST API Framework

- [ ] T013 Create REST API base controller in `includes/api/class-wpc-rest-controller.php`
- [ ] T014 [P] Create upload endpoint in `includes/api/class-wpc-upload-endpoint.php`
- [ ] T015 [P] Create design save/load endpoint in `includes/api/class-wpc-design-endpoint.php`
- [ ] T016 [P] Create price calculation endpoint in `includes/api/class-wpc-price-endpoint.php`

### Admin Foundation

- [ ] T017 Create admin controller class in `includes/admin/class-wpc-admin.php`
- [ ] T018 [P] Create plugin settings page in `includes/admin/class-wpc-settings.php`
- [ ] T019 [P] Create product meta box handler in `includes/admin/class-wpc-product-meta.php`

### Frontend Foundation

- [ ] T020 Create frontend controller in `includes/frontend/class-wpc-frontend.php`
- [ ] T021 Create customizer loader (determines which customizer to load) in `includes/frontend/class-wpc-customizer-loader.php`
- [ ] T022 Create base customizer abstract class in `includes/customizers/class-wpc-base-customizer.php`

### JavaScript Foundation

- [ ] T023 Create Alpine.js main app initialization in `assets/js/customizer/app.js`
- [ ] T024 [P] Create canvas helper utilities (Fabric.js) in `assets/js/customizer/utils/canvas-helpers.js`
- [ ] T025 [P] Create Three.js helper utilities in `assets/js/customizer/utils/three-helpers.js`
- [ ] T026 [P] Create localStorage auto-save utility in `assets/js/customizer/utils/storage.js`

### Shared Components

- [ ] T027 [P] Create 2D preview component in `assets/js/customizer/components/preview-2d.js`
- [ ] T028 [P] Create 3D preview component in `assets/js/customizer/components/preview-3d.js`
- [ ] T029 [P] Create text editor component in `assets/js/customizer/components/text-editor.js`
- [ ] T030 [P] Create image uploader component in `assets/js/customizer/components/image-uploader.js`
- [ ] T031 [P] Create color picker component in `assets/js/customizer/components/color-picker.js`
- [ ] T032 [P] Create price display component in `assets/js/customizer/components/price-display.js`

### Stylesheets

- [ ] T033 [P] Create main customizer stylesheet in `assets/css/customizer.css`
- [ ] T034 [P] Create responsive styles in `assets/css/responsive.css`
- [ ] T035 [P] Create admin styles in `assets/css/admin.css`

### Templates

- [ ] T036 Create main customizer template in `templates/customizer/main.php`
- [ ] T037 [P] Create preview area partial in `templates/customizer/partials/preview-area.php`
- [ ] T038 [P] Create controls panel partial in `templates/customizer/partials/controls-panel.php`
- [ ] T039 [P] Create zone tabs partial in `templates/customizer/partials/zone-tabs.php`
- [ ] T040 [P] Create layer panel partial in `templates/customizer/partials/layer-panel.php`

**Checkpoint**: Foundation ready - user story implementation can now begin

---

## Phase 3: User Story 1 - Neon Sign Customizer (Priority: P1) 🎯 MVP

**Goal**: Customer can create personalized neon sign with custom text, color, font, size, and background with real-time preview and pricing

**Independent Test**: Create a neon sign with custom text "Happy Birthday", select blue color, choose size Large, verify preview updates and correct price in cart

### Implementation for User Story 1

- [ ] T041 [US1] Create Neon customizer class extending base in `includes/customizers/class-wpc-neon-customizer.php`
- [ ] T042 [US1] Define neon color options (6+ colors) and glow settings in `includes/customizers/class-wpc-neon-customizer.php`
- [ ] T043 [US1] Define neon font options (12 styles: Script, Vibes, Elegant, etc.) in `includes/customizers/class-wpc-neon-customizer.php`
- [ ] T044 [US1] Define size options (Small, Medium, Large, X-Large) with pricing in `includes/customizers/class-wpc-neon-customizer.php`
- [ ] T045 [US1] Define background options (brick, wood, dark, none) in `includes/customizers/class-wpc-neon-customizer.php`
- [ ] T046 [US1] Create neon-specific JavaScript logic in `assets/js/customizer/customizers/neon.js`
- [ ] T047 [US1] Implement real-time neon glow effect using CSS/Canvas in `assets/js/customizer/customizers/neon.js`
- [ ] T048 [US1] Create neon controls template in `templates/customizer/product-types/neon.php`
- [ ] T049 [US1] Implement neon price calculation (size multipliers, character count) in `includes/models/class-wpc-price-calculator.php`
- [ ] T050 [US1] Add quantity selector with price updates in `assets/js/customizer/customizers/neon.js`
- [ ] T051 [US1] Add fullscreen preview modal for neon in `assets/js/customizer/customizers/neon.js`
- [ ] T052 [US1] Integrate Google Fonts for 12 neon font styles in `assets/css/customizer.css`

**Checkpoint**: User Story 1 (Neon Sign) should be fully functional and testable independently

---

## Phase 4: User Story 2 - Mug Image Upload & 3D Preview (Priority: P1)

**Goal**: Customer can upload image to mug zones, position it, preview in 3D, and add to cart

**Independent Test**: Upload image to front zone of 3-zone mug, scale to 50%, rotate 3D preview to see all zones, add to cart with image preserved

### Implementation for User Story 2

- [ ] T053 [US2] Create Mug customizer class in `includes/customizers/class-wpc-mug-customizer.php`
- [ ] T054 [US2] Define 3-zone configuration (Front: 3.125"w, Back: 3.125"w, Rear: 1.5"w, Height: 3.75") in `includes/customizers/class-wpc-mug-customizer.php`
- [ ] T055 [US2] Define full-wrap configuration (7.75"w x 3.75"h) in `includes/customizers/class-wpc-mug-customizer.php`
- [ ] T056 [US2] Create mug-specific JavaScript logic in `assets/js/customizer/customizers/mug.js`
- [ ] T057 [US2] Implement drag-and-drop image upload per zone in `assets/js/customizer/customizers/mug.js`
- [ ] T058 [US2] Implement image scaling and positioning controls in `assets/js/customizer/customizers/mug.js`
- [ ] T059 [US2] Create 3D mug model with UV mapping in `assets/models/mug-standard.glb`
- [ ] T060 [US2] Create heart-handle mug model in `assets/models/mug-heart-handle.glb`
- [ ] T061 [US2] Implement Three.js 3D preview with rotation in `assets/js/customizer/customizers/mug.js`
- [ ] T062 [US2] Apply uploaded image as texture to 3D model in `assets/js/customizer/customizers/mug.js`
- [ ] T063 [US2] Implement text layer support per zone in `assets/js/customizer/customizers/mug.js`
- [ ] T064 [US2] Create mug controls template in `templates/customizer/product-types/mug.php`
- [ ] T065 [US2] Add fullscreen preview modal for mug in `assets/js/customizer/customizers/mug.js`
- [ ] T066 [US2] Implement mug price calculation (image upload fee, text layers) in `includes/models/class-wpc-price-calculator.php`

**Checkpoint**: User Story 2 (Mug) should be fully functional and testable independently

---

## Phase 5: User Story 3 - Visiting Card Designer (Priority: P2)

**Goal**: Customer can design front/back of visiting card with logo upload, text fields, paper finish, and quantity pricing

**Independent Test**: Enter contact details, upload logo, select gloss finish, set quantity to 500, preview front/back flip, verify quantity pricing applied

### Implementation for User Story 3

- [ ] T067 [US3] Create Card customizer class in `includes/customizers/class-wpc-card-customizer.php`
- [ ] T068 [US3] Define card zones (front/back) in `includes/customizers/class-wpc-card-customizer.php`
- [ ] T069 [US3] Define paper finish options (matte, gloss, textured) in `includes/customizers/class-wpc-card-customizer.php`
- [ ] T070 [US3] Define corner style options (square, rounded) in `includes/customizers/class-wpc-card-customizer.php`
- [ ] T071 [US3] Create card-specific JavaScript logic in `assets/js/customizer/customizers/card.js`
- [ ] T072 [US3] Implement text fields (name, title, phone, email, address) with positioning in `assets/js/customizer/customizers/card.js`
- [ ] T073 [US3] Implement logo upload with position selection in `assets/js/customizer/customizers/card.js`
- [ ] T074 [US3] Implement front/back card image upload mode in `assets/js/customizer/customizers/card.js`
- [ ] T075 [US3] Implement card flip animation for preview in `assets/js/customizer/customizers/card.js`
- [ ] T076 [US3] Create card controls template in `templates/customizer/product-types/card.php`
- [ ] T077 [US3] Implement quantity-based tiered pricing (100/250/500/1000) in `includes/models/class-wpc-price-calculator.php`
- [ ] T078 [US3] Add card template selection (if templates provided) in `assets/js/customizer/customizers/card.js`

**Checkpoint**: User Story 3 (Visiting Card) should be fully functional and testable independently

---

## Phase 6: User Story 4 - Multi-Layer Text (Priority: P2)

**Goal**: Customer can add multiple text layers with independent styling to any product zone

**Independent Test**: Add 3 text layers to mug front zone, style each with different font/color/size, reposition them, verify all appear correctly in preview

### Implementation for User Story 4

- [ ] T079 [US4] Extend text editor component for multi-layer support in `assets/js/customizer/components/text-editor.js`
- [ ] T080 [US4] Implement layer panel with add/remove/reorder in `assets/js/customizer/components/text-editor.js`
- [ ] T081 [US4] Implement per-layer styling (font, size, color) in `assets/js/customizer/components/text-editor.js`
- [ ] T082 [US4] Implement layer selection and highlighting in `assets/js/customizer/components/text-editor.js`
- [ ] T083 [US4] Implement layer positioning with drag in `assets/js/customizer/components/text-editor.js`
- [ ] T084 [US4] Update layer panel template in `templates/customizer/partials/layer-panel.php`
- [ ] T085 [US4] Implement text layer price modifier (per-layer fee) in `includes/models/class-wpc-price-calculator.php`

**Checkpoint**: User Story 4 (Multi-Layer Text) works with all applicable products

---

## Phase 7: User Story 5 - T-Shirt Customizer (Priority: P2)

**Goal**: Customer can design t-shirt with front/back/sleeve zones, upload images, select color/size, and preview

**Independent Test**: Upload image to front, add text to back, select black color, XL size, preview all zones, verify all options in cart

### Implementation for User Story 5

- [ ] T086 [US5] Create T-Shirt customizer class in `includes/customizers/class-wpc-tshirt-customizer.php`
- [ ] T087 [US5] Define 4 zones (front, back, left sleeve, right sleeve) in `includes/customizers/class-wpc-tshirt-customizer.php`
- [ ] T088 [US5] Define color variants (5+ colors: black, white, navy, red, gray) in `includes/customizers/class-wpc-tshirt-customizer.php`
- [ ] T089 [US5] Define size options (XS, S, M, L, XL, XXL) in `includes/customizers/class-wpc-tshirt-customizer.php`
- [ ] T090 [US5] Create t-shirt-specific JavaScript logic in `assets/js/customizer/customizers/tshirt.js`
- [ ] T091 [US5] Implement zone-based image upload in `assets/js/customizer/customizers/tshirt.js`
- [ ] T092 [US5] Implement zone-based text support in `assets/js/customizer/customizers/tshirt.js`
- [ ] T093 [US5] Implement color variant switching with preview update in `assets/js/customizer/customizers/tshirt.js`
- [ ] T094 [US5] Create 3D t-shirt model (or 2D multi-view) in `assets/models/tshirt.glb`
- [ ] T095 [US5] Create t-shirt controls template in `templates/customizer/product-types/tshirt.php`
- [ ] T096 [US5] Add fullscreen preview modal for t-shirt in `assets/js/customizer/customizers/tshirt.js`
- [ ] T097 [US5] Implement t-shirt price calculation (size modifier) in `includes/models/class-wpc-price-calculator.php`

**Checkpoint**: User Story 5 (T-Shirt) should be fully functional and testable independently

---

## Phase 8: User Story 6 - Mobile Experience (Priority: P2)

**Goal**: Mobile customers can complete full customization flow with touch gestures and optimized layout

**Independent Test**: On mobile device, load mug customizer, swipe to rotate 3D, upload from gallery, complete add-to-cart

### Implementation for User Story 6

- [ ] T098 [US6] Implement stacked mobile layout (preview top, controls below) in `assets/css/responsive.css`
- [ ] T099 [US6] Implement touch gestures for 3D rotation in `assets/js/customizer/components/preview-3d.js`
- [ ] T100 [US6] Optimize touch targets for mobile (min 44px) in `assets/css/responsive.css`
- [ ] T101 [US6] Implement mobile-friendly file picker with camera option in `assets/js/customizer/components/image-uploader.js`
- [ ] T102 [US6] Optimize 3D model loading for mobile (lower poly, lazy load) in `assets/js/customizer/components/preview-3d.js`
- [ ] T103 [US6] Implement 2D fallback detection for low-end devices in `assets/js/customizer/components/preview-3d.js`
- [ ] T104 [US6] Test and fix all customizers on 320px width in `assets/css/responsive.css`

**Checkpoint**: All customizers work fully on mobile devices

---

## Phase 9: User Story 7 - Admin Product Configuration (Priority: P3)

**Goal**: Admin can enable customizer on products, select type, configure zones and pricing

**Independent Test**: Edit product in WooCommerce, enable customizer, select Mug (3-Zone), save, verify customizer appears on frontend

### Implementation for User Story 7

- [ ] T105 [US7] Create product meta box UI in `includes/admin/class-wpc-product-meta.php`
- [ ] T106 [US7] Implement customizer type dropdown in `includes/admin/class-wpc-product-meta.php`
- [ ] T107 [US7] Implement zone configuration UI per type in `includes/admin/class-wpc-product-meta.php`
- [ ] T108 [US7] Implement price modifier configuration in `includes/admin/class-wpc-product-meta.php`
- [ ] T109 [US7] Create admin JavaScript for meta box in `assets/js/admin/product-meta.js`
- [ ] T110 [US7] Save product meta with sanitization in `includes/admin/class-wpc-product-meta.php`
- [ ] T111 [US7] Load saved configuration on frontend in `includes/frontend/class-wpc-customizer-loader.php`

**Checkpoint**: Admin can configure any product with customizer

---

## Phase 10: User Story 8 - Order Design Visibility (Priority: P3)

**Goal**: Customer and admin can view customization details in order history and admin orders

**Independent Test**: Place order with custom mug, view in account order history, verify thumbnail and options visible

### Implementation for User Story 8

- [ ] T112 [US8] Create order display class in `includes/admin/class-wpc-order-display.php`
- [ ] T113 [US8] Store design data in order item meta in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T114 [US8] Display customization in cart in `templates/cart/customization-details.php`
- [ ] T115 [US8] Display customization in checkout in `templates/cart/customization-details.php`
- [ ] T116 [US8] Display customization in order confirmation in `includes/admin/class-wpc-order-display.php`
- [ ] T117 [US8] Display customization in customer order history in `includes/admin/class-wpc-order-display.php`
- [ ] T118 [US8] Display customization in admin order view in `includes/admin/class-wpc-order-display.php`
- [ ] T119 [US8] Include customization in order emails in `templates/emails/customization-details.php`
- [ ] T120 [US8] Generate and store design thumbnail for order in `includes/frontend/class-wpc-cart-handler.php`

**Checkpoint**: Customization visible throughout order lifecycle

---

## Phase 11: Remaining Product Types (Priority: P3)

**Goal**: Implement remaining 6 product customizers using established patterns

### Tumbler Customizer

- [ ] T121 [P] Create Tumbler customizer class in `includes/customizers/class-wpc-tumbler-customizer.php`
- [ ] T122 [P] Create tumbler JavaScript logic in `assets/js/customizer/customizers/tumbler.js`
- [ ] T123 [P] Create tumbler 3D model in `assets/models/tumbler.glb`
- [ ] T124 [P] Create tumbler template in `templates/customizer/product-types/tumbler.php`

### Bottle Customizer

- [ ] T125 [P] Create Bottle customizer class in `includes/customizers/class-wpc-bottle-customizer.php`
- [ ] T126 [P] Create bottle JavaScript logic in `assets/js/customizer/customizers/bottle.js`
- [ ] T127 [P] Create bottle 3D model in `assets/models/bottle.glb`
- [ ] T128 [P] Create bottle template in `templates/customizer/product-types/bottle.php`

### Pen Customizer

- [ ] T129 [P] Create Pen customizer class in `includes/customizers/class-wpc-pen-customizer.php`
- [ ] T130 [P] Create pen JavaScript logic in `assets/js/customizer/customizers/pen.js`
- [ ] T131 [P] Create pen template in `templates/customizer/product-types/pen.php`

### Bag Customizer

- [ ] T132 [P] Create Bag customizer class in `includes/customizers/class-wpc-bag-customizer.php`
- [ ] T133 [P] Create bag JavaScript logic in `assets/js/customizer/customizers/bag.js`
- [ ] T134 [P] Create bag template in `templates/customizer/product-types/bag.php`

### Keychain Customizer

- [ ] T135 [P] Create Keychain customizer class in `includes/customizers/class-wpc-keychain-customizer.php`
- [ ] T136 [P] Create keychain JavaScript logic in `assets/js/customizer/customizers/keychain.js`
- [ ] T137 [P] Create keychain template in `templates/customizer/product-types/keychain.php`

### Cap Customizer

- [ ] T138 [P] Create Cap customizer class in `includes/customizers/class-wpc-cap-customizer.php`
- [ ] T139 [P] Create cap JavaScript logic in `assets/js/customizer/customizers/cap.js`
- [ ] T140 [P] Create cap template in `templates/customizer/product-types/cap.php`

**Checkpoint**: All 12 product types implemented

---

## Phase 12: WooCommerce Cart Integration

**Purpose**: Complete cart/checkout integration for all products

- [ ] T141 Create cart handler class in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T142 Implement add-to-cart with design data in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T143 Implement cart item display with customization in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T144 Implement cart item edit (return to customizer) in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T145 Implement design validation before checkout in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T146 Store design files on order completion in `includes/frontend/class-wpc-cart-handler.php`

---

## Phase 13: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

### File Upload & Validation

- [ ] T147 Implement file type validation (JPEG, PNG, PDF only) in `includes/api/class-wpc-upload-endpoint.php`
- [ ] T148 Implement file size validation (10MB max) in `includes/api/class-wpc-upload-endpoint.php`
- [ ] T149 Implement upload progress indicator in `assets/js/customizer/components/image-uploader.js`
- [ ] T150 Implement client-side image compression in `assets/js/customizer/components/image-uploader.js`

### Auto-Save & Session

- [ ] T151 Implement localStorage auto-save in `assets/js/customizer/utils/storage.js`
- [ ] T152 Implement session backup on server in `includes/frontend/class-wpc-cart-handler.php`
- [ ] T153 Implement design restore on page return in `assets/js/customizer/app.js`

### Error Handling

- [ ] T154 [P] Implement 3D to 2D fallback gracefully in `assets/js/customizer/components/preview-3d.js`
- [ ] T155 [P] Implement upload error messaging in `assets/js/customizer/components/image-uploader.js`
- [ ] T156 [P] Implement character limit validation for text in `assets/js/customizer/components/text-editor.js`

### Performance

- [ ] T157 Implement lazy loading of 3D models in `assets/js/customizer/components/preview-3d.js`
- [ ] T158 Implement debounced preview updates in `assets/js/customizer/app.js`
- [ ] T159 Optimize CSS and JS bundle sizes in `assets/`

### Security

- [ ] T160 Implement nonce verification on all API endpoints in `includes/api/class-wpc-rest-controller.php`
- [ ] T161 Sanitize all user inputs in `includes/api/class-wpc-rest-controller.php`
- [ ] T162 Validate file integrity on upload in `includes/api/class-wpc-upload-endpoint.php`

### Translation

- [ ] T163 Add all strings to translation domain in all PHP files
- [ ] T164 Generate POT file in `languages/woo-product-customizer.pot`

---

## Dependencies & Execution Order

### Phase Dependencies

```
Setup (Phase 1)
    └── Foundational (Phase 2) ⚠️ BLOCKS ALL STORIES
            ├── US1: Neon Sign (Phase 3) 🎯 MVP
            ├── US2: Mug (Phase 4)
            ├── US3: Visiting Card (Phase 5)
            ├── US4: Multi-Layer Text (Phase 6)
            ├── US5: T-Shirt (Phase 7)
            ├── US6: Mobile (Phase 8)
            ├── US7: Admin Config (Phase 9)
            ├── US8: Order Display (Phase 10)
            ├── Remaining Products (Phase 11)
            └── Cart Integration (Phase 12)
                    └── Polish (Phase 13)
```

### User Story Dependencies

| Story | Depends On | Can Parallel With |
|-------|------------|-------------------|
| US1 (Neon) | Foundational only | US2, US3 |
| US2 (Mug) | Foundational only | US1, US3 |
| US3 (Card) | Foundational only | US1, US2 |
| US4 (Multi-Text) | Foundational only | Any |
| US5 (T-Shirt) | Foundational only | US1-US4 |
| US6 (Mobile) | US1-US5 (needs products to test) | - |
| US7 (Admin) | Foundational only | US1-US5 |
| US8 (Orders) | Cart Integration | - |

### Within Each User Story

1. PHP customizer class first
2. JavaScript logic second
3. Templates third
4. Price calculation last

### Parallel Opportunities

**Setup Phase (all [P] tasks):**
```
T003 (loader) || T004 (activator) || T005 (deactivator) || T006 (composer) || T007 (package)
```

**Foundational Phase (grouped):**
```
# Models parallel:
T010 (Design) || T011 (TextLayer) || T012 (PriceCalc)

# API parallel:
T014 (upload) || T015 (design) || T016 (price)

# Admin parallel:
T018 (settings) || T019 (product-meta)

# Components parallel:
T027 (2D) || T028 (3D) || T029 (text) || T030 (upload) || T031 (color) || T032 (price)

# Styles parallel:
T033 (customizer) || T034 (responsive) || T035 (admin)

# Templates parallel:
T037 (preview) || T038 (controls) || T039 (tabs) || T040 (layers)
```

**User Stories (after Foundational):**
```
US1 (Neon) || US2 (Mug) || US3 (Card) can all start simultaneously
```

**Remaining Products (Phase 11):**
```
Tumbler || Bottle || Pen || Bag || Keychain || Cap - all parallel
```

---

## Parallel Example: Foundational Components

```bash
# Launch all shared components in parallel:
Task: "Create 2D preview component in assets/js/customizer/components/preview-2d.js"
Task: "Create 3D preview component in assets/js/customizer/components/preview-3d.js"
Task: "Create text editor component in assets/js/customizer/components/text-editor.js"
Task: "Create image uploader component in assets/js/customizer/components/image-uploader.js"
Task: "Create color picker component in assets/js/customizer/components/color-picker.js"
Task: "Create price display component in assets/js/customizer/components/price-display.js"
```

---

## Implementation Strategy

### MVP First (User Story 1: Neon Sign Only)

1. Complete Phase 1: Setup (T001-T008)
2. Complete Phase 2: Foundational (T009-T040)
3. Complete Phase 3: User Story 1 - Neon Sign (T041-T052)
4. **STOP and VALIDATE**: Test Neon Sign customizer end-to-end
5. Deploy/demo if ready

### Incremental Delivery

1. **Milestone 1**: Setup + Foundational → Foundation ready
2. **Milestone 2**: Add Neon Sign → MVP ready for demo
3. **Milestone 3**: Add Mug + Visiting Card → Core products complete
4. **Milestone 4**: Add T-Shirt + Multi-text → Full merchandise line
5. **Milestone 5**: Add Mobile + Admin → Production ready
6. **Milestone 6**: Add Orders + Remaining products → Full feature complete

### Suggested MVP Scope

**Minimum Viable Product = Neon Sign Only**
- 40 tasks (T001-T040 foundation + T041-T052 neon)
- Demonstrates full customization flow
- Real-time preview, pricing, cart integration
- Can generate revenue immediately

---

## Summary

| Metric | Count |
|--------|-------|
| **Total Tasks** | 164 |
| **Setup Phase** | 8 |
| **Foundational Phase** | 32 |
| **User Story 1 (Neon)** | 12 |
| **User Story 2 (Mug)** | 14 |
| **User Story 3 (Card)** | 12 |
| **User Story 4 (Multi-Text)** | 7 |
| **User Story 5 (T-Shirt)** | 12 |
| **User Story 6 (Mobile)** | 7 |
| **User Story 7 (Admin)** | 7 |
| **User Story 8 (Orders)** | 9 |
| **Remaining Products** | 20 |
| **Cart Integration** | 6 |
| **Polish Phase** | 18 |
| **Parallel Opportunities** | 60+ tasks marked [P] |

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- All product customizers follow same pattern: PHP class → JS logic → Template → Pricing
