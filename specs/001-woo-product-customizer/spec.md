# Feature Specification: WooCommerce Product Customizer Plugin

**Feature Branch**: `001-woo-product-customizer`
**Created**: 2026-02-03
**Status**: Draft
**Input**: WooCommerce Product Customizer Plugin with 12 product types for custom printing/merchandise business

---

## Overview

A WooCommerce plugin that enables customers to personalize products with custom designs, text, and images before purchase. The plugin supports 12 product types across 3 categories: Custom Signage (Neon Signs), Print Products (Visiting Cards), and Merchandise (Mugs, Apparel, Accessories).

---

## Product Categories & Types

### Category 1: Custom Signage

| # | Product | Customization Features |
|---|---------|----------------------|
| 1 | **Neon Sign** | Text input, neon color selection, font style, glow intensity, background selection (brick/wood/dark/none), size options |

### Category 2: Print Products

| # | Product | Customization Features |
|---|---------|----------------------|
| 2 | **Visiting Card** | Front/back design, logo upload, text fields (name, title, phone, email, address), template selection, paper finish (matte/gloss/textured), corner style (square/rounded) |

### Category 3: Merchandise

| # | Product | Customization Features |
|---|---------|----------------------|
| 3 | **Mug (3-Zone)** | Front zone (3.125"w), Back zone (3.125"w), Rear/Handle zone (1.5"w), image upload per zone, text overlay, 3D preview |
| 4 | **Mug (Full Wrap)** | Single wraparound image (7.75"w x 3.75"h), text overlay, 3D preview |
| 5 | **Heart Handle Mug** | Front/back image upload, text overlay, handle color selection, 3D preview |
| 6 | **Tumbler** | Front/back design zones, image upload, text overlay, 3D preview |
| 7 | **Bottle** | Front/back design zones, image upload, text overlay, 3D preview |
| 8 | **T-Shirt** | Front/back/sleeve zones, image upload, text overlay, size selection, color variants |
| 9 | **Pen** | Barrel print zone, text/logo, color variants |
| 10 | **Bags** | Multiple bag types, front/back zones, image upload, text overlay |
| 11 | **Keychain** | Shape selection, front/back design, visualization preview only |
| 12 | **Cap** | Front embroidery zone, image/text, color variants |

---

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Customer Designs a Custom Neon Sign (Priority: P1)

A customer visits the neon sign product page and wants to create a personalized neon sign with their name or custom text. They enter their text, select a neon color (pink, blue, green, etc.), choose a font style, pick a background for preview, select size, and see real-time price updates before adding to cart.

**Why this priority**: Neon signs are the primary high-value product. This story establishes the core customization flow that applies to all products.

**Independent Test**: Can be fully tested by creating a neon sign with custom text and verifying it appears correctly in cart with all customization details preserved.

**Acceptance Scenarios**:

1. **Given** customer is on neon sign product page, **When** they enter "Happy Birthday" as text, **Then** the preview shows glowing text with default color (pink)
2. **Given** customer has entered text, **When** they select blue color, **Then** preview updates immediately to show blue neon glow
3. **Given** customer has configured design, **When** they select "Large" size, **Then** price updates from base to large pricing
4. **Given** design is complete, **When** customer clicks "Add to Cart", **Then** cart shows product with all customization details (text, color, font, size)

---

### User Story 2 - Customer Uploads Image to Mug (Priority: P1)

A customer wants to create a personalized mug with their photo. They upload an image, position it on the mug's front zone, optionally add text overlay, preview in 3D by rotating the mug, and add to cart.

**Why this priority**: Image upload with 3D preview is the core differentiator and applies to most merchandise products.

**Independent Test**: Can be tested by uploading an image to a mug, rotating 3D preview, and verifying image appears in cart/order.

**Acceptance Scenarios**:

1. **Given** customer is on mug product page, **When** they drag-drop a JPG image, **Then** image appears in the front zone preview
2. **Given** image is uploaded, **When** customer uses scale slider, **Then** image size adjusts in real-time on preview
3. **Given** image is positioned, **When** customer drags 3D preview, **Then** mug rotates showing all zones
4. **Given** customer switches to "Back" zone tab, **When** they upload second image, **Then** back zone shows new image while front retains original

---

### User Story 3 - Customer Designs Visiting Card (Priority: P2)

A business professional wants to order custom visiting cards. They enter their contact details, upload company logo, select a template or start blank, choose paper finish and corner style, preview both front and back, and place order.

**Why this priority**: Visiting cards are a recurring B2B product with high order volume potential.

**Independent Test**: Can be tested by filling all card fields, uploading logo, previewing flip animation, and verifying all data in order.

**Acceptance Scenarios**:

1. **Given** customer is on visiting card page, **When** they enter name and phone, **Then** preview card shows entered text in designated positions
2. **Given** customer has entered details, **When** they click "Back" tab, **Then** card flips to show back design
3. **Given** customer uploads logo PNG, **When** they select "Bottom Right" position, **Then** logo appears in that corner of preview
4. **Given** design complete, **When** customer selects "Gloss" finish and 500 quantity, **Then** price updates accordingly

---

### User Story 4 - Customer Adds Multi-Layer Text to Product (Priority: P2)

A customer wants to add multiple text elements to their product (e.g., name on top, date below). They add text layers, customize each with different fonts/colors/sizes, position them, and see combined preview.

**Why this priority**: Multi-layer text is a key feature differentiating from basic customizers.

**Independent Test**: Can be tested by adding 3 text layers with different styles and verifying all appear correctly in preview and order.

**Acceptance Scenarios**:

1. **Given** customer is customizing mug, **When** they click "Add Text", **Then** new text layer appears in layer panel
2. **Given** text layer exists, **When** they type "John's 50th", **Then** text appears on product preview
3. **Given** one text layer exists, **When** they click "Add Text" again, **Then** second independent layer is created
4. **Given** multiple layers exist, **When** they select layer 2 and change color to red, **Then** only layer 2 changes color

---

### User Story 5 - Customer Customizes T-Shirt (Priority: P2)

A customer wants to design a custom t-shirt with front design, back design, and select size/color. They upload images to front/back zones, add text, select shirt size (S-XXL), choose shirt color, and preview before ordering.

**Why this priority**: T-shirts have broad appeal and demonstrate multi-zone customization.

**Independent Test**: Can be tested by designing front and back, selecting size XL and black color, verifying all in cart.

**Acceptance Scenarios**:

1. **Given** customer is on t-shirt page, **When** they select "Black" color variant, **Then** preview shows black t-shirt
2. **Given** black shirt selected, **When** they upload white logo to front, **Then** logo appears on front zone of black shirt
3. **Given** front designed, **When** they switch to "Back" tab, **Then** view changes to back of shirt
4. **Given** design complete, **When** they select "XL" size, **Then** size is recorded and price may adjust

---

### User Story 6 - Store Admin Enables Customizer on Product (Priority: P3)

A store administrator wants to enable the customizer on a new product. They edit the product in WooCommerce, enable customizer, select customizer type, configure zones and pricing modifiers.

**Why this priority**: Admin configuration is essential but happens less frequently than customer interactions.

**Independent Test**: Can be tested by enabling customizer on test product and verifying it appears on frontend.

**Acceptance Scenarios**:

1. **Given** admin is editing product in WooCommerce, **When** they check "Enable Customizer", **Then** customizer options panel appears
2. **Given** customizer enabled, **When** they select "Mug (3-Zone)" type, **Then** zone configuration options appear
3. **Given** type selected, **When** they save product, **Then** frontend product page shows customizer interface

---

### User Story 7 - Mobile Customer Designs Product (Priority: P2)

A customer on mobile phone wants to customize a product. They see mobile-optimized layout with stacked preview/controls, use touch gestures for 3D rotation, upload image from phone gallery, and complete order.

**Why this priority**: Significant portion of e-commerce traffic is mobile; poor mobile experience loses sales.

**Independent Test**: Can be tested on mobile device by completing full customization flow with touch interactions.

**Acceptance Scenarios**:

1. **Given** customer opens product page on mobile, **When** page loads, **Then** preview area is prominent at top, controls below
2. **Given** mobile layout shown, **When** customer swipes on 3D preview, **Then** product rotates smoothly
3. **Given** customer taps upload, **When** phone gallery opens and they select photo, **Then** image uploads and appears on product
4. **Given** mobile customization complete, **When** customer taps "Add to Cart", **Then** product adds successfully

---

### User Story 8 - Customer Views Order with Custom Design (Priority: P3)

A customer who placed an order wants to view their custom design details in their order history. They see thumbnail of their design, all customization options they selected, and can contact support if needed.

**Why this priority**: Post-purchase visibility builds trust and reduces support inquiries.

**Independent Test**: Can be tested by placing order with customization and viewing it in account order history.

**Acceptance Scenarios**:

1. **Given** customer placed order with custom mug, **When** they view order in account, **Then** they see customization details listed
2. **Given** order has uploaded image, **When** viewing order details, **Then** thumbnail of uploaded design is visible
3. **Given** order has text customization, **When** viewing details, **Then** text content, font, and color are shown

---

### Edge Cases

- **Large file upload**: When customer uploads image larger than 10MB, show error message with size limit and suggest compression
- **Text length exceeded**: When customer enters text longer than maximum characters, prevent input beyond limit and show remaining character count
- **Unsupported format**: When customer uploads unsupported file format (e.g., .tiff, .bmp), show error specifying accepted formats (JPEG, PNG, PDF)
- **3D model failure**: When 3D model fails to load, fall back to 2D multi-angle preview with clear messaging
- **Session interrupted**: When customer leaves page mid-design, auto-save design to browser storage and restore on return
- **Special characters**: When customer enters emoji or special unicode in text, accept standard unicode but warn about print limitations for emoji
- **Product disabled**: When customer has customized product in cart but product is later disabled, show notification and allow removal from cart
- **Empty design submission**: When customer tries to add to cart with no customization (no text, no image), prompt them to add at least one element
- **Concurrent editing**: When same design is open in multiple browser tabs, most recent save wins with timestamp

---

## Requirements *(mandatory)*

### Functional Requirements

#### Core Customizer Engine

- **FR-001**: System MUST provide real-time visual preview of all customizations as user makes changes
- **FR-002**: System MUST support image upload in JPEG, PNG, and PDF formats up to 10MB
- **FR-003**: System MUST allow multiple text layers (minimum 3) per design zone
- **FR-004**: System MUST provide text styling options: font family, font size, text color
- **FR-005**: System MUST calculate and display price updates in real-time as options change
- **FR-006**: System MUST preserve all customization data when product is added to cart

#### Product-Specific Features

- **FR-007**: Neon Sign customizer MUST support: text input (max 25 chars), 6+ color options, 3+ font styles, 4 background options, 4 size options
- **FR-008**: Visiting Card customizer MUST support: front/back design, logo upload with positioning, text fields, 3 paper finish options, 2 corner styles
- **FR-009**: Mug customizer MUST support: 3-zone mode (front/back/rear) and full-wrap mode, 3D preview rotation
- **FR-010**: T-Shirt customizer MUST support: front/back/sleeve zones, 5+ color variants, standard size range (XS-XXL)
- **FR-011**: Keychain customizer MUST provide visualization preview (non-printable preview only per requirements)
- **FR-012**: Tumbler and Bottle customizers MUST support: front/back zones, image upload, 3D preview
- **FR-013**: Pen customizer MUST support: barrel text/logo zone, color variants
- **FR-014**: Bags customizer MUST support: multiple bag type selection, front/back zones
- **FR-015**: Cap customizer MUST support: front embroidery zone, color variants

#### User Interface

- **FR-016**: System MUST be fully responsive and functional on mobile devices (minimum 320px width)
- **FR-017**: System MUST provide 3D product preview with rotation capability for applicable products (mugs, bottles, tumblers)
- **FR-018**: System MUST provide 2D fallback preview when 3D is unavailable or fails
- **FR-019**: System MUST show upload progress indicator during file upload
- **FR-020**: System MUST provide undo capability for design changes
- **FR-021**: System MUST auto-save designs to prevent loss during browser refresh or accidental navigation

#### WooCommerce Integration

- **FR-022**: System MUST integrate with WooCommerce cart and preserve all customization data
- **FR-023**: System MUST store customization details in order meta for fulfillment
- **FR-024**: System MUST display customization summary in cart, checkout, and order confirmation
- **FR-025**: System MUST include customization details in order emails (customer and admin)
- **FR-026**: System MUST provide admin interface to view customer designs per order

#### Data & Storage

- **FR-027**: System MUST securely store uploaded design files associated with orders
- **FR-028**: System MUST retain design files for minimum 90 days after order completion
- **FR-029**: System MUST validate uploaded files for type, size, and basic integrity

---

### Key Entities

- **Product Configuration**: Customizer type, enabled zones, pricing modifiers, available options per product
- **Customer Design**: Selected options (text, colors, fonts, sizes), uploaded images, zone assignments, timestamps
- **Design File**: Uploaded image reference, storage location, file metadata, associated order
- **Price Modifier**: Rules for calculating final price based on customization choices (size, zones used, image uploads)
- **Text Layer**: Text content, font family, font size, color, position within zone

---

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Customers can complete product customization (from page load to add-to-cart) in under 3 minutes for simple designs
- **SC-002**: Preview updates appear within 500ms of user input (text, color, image positioning)
- **SC-003**: 95% of image uploads complete successfully without user retry
- **SC-004**: Mobile customization flow is completable with same functionality as desktop
- **SC-005**: System handles 100 concurrent customization sessions without degradation
- **SC-006**: Page load time for customizer products remains under 3 seconds on standard connections
- **SC-007**: Cart abandonment rate for customizer products is equal to or lower than standard products
- **SC-008**: Customer support tickets related to "design not saved" or "customization lost" are below 1% of orders
- **SC-009**: 90% of customers can successfully upload an image on first attempt
- **SC-010**: Order fulfillment team can access all design files and specifications for 100% of custom orders

---

## Assumptions

1. **File Storage**: Uploaded design files will be stored on the web server's file system in a dedicated uploads directory. Cloud storage integration is out of scope for initial release.

2. **3D Models**: Pre-built 3D models (GLB/GLTF format) for products requiring 3D preview will be provided/created as part of implementation.

3. **Print Production**: The plugin handles customer-facing design and order capture only. Print file generation for production is handled by separate fulfillment systems.

4. **Payment**: Standard WooCommerce payment gateways are used; no custom payment integration required.

5. **User Authentication**: Guest checkout is supported; designs are tied to session/cart, not user accounts.

6. **Browser Support**: Modern browsers (Chrome, Firefox, Safari, Edge - last 2 versions) are supported. IE11 is not supported.

7. **Quantity Pricing**: Visiting cards have quantity-based pricing tiers. Other products are single-unit customization.

8. **Font Licensing**: Web-safe fonts and Google Fonts will be used to avoid licensing issues.

9. **Single Language**: Initial release supports English only. Multi-language support is future enhancement.

10. **Standard WooCommerce Theme Compatibility**: Plugin designed to work with standard WooCommerce-compatible themes without requiring theme modifications.

---

## Constraints

- Must work within WooCommerce plugin architecture and hooks
- Must not conflict with common WooCommerce themes (Storefront, Flatsome, Astra)
- Image uploads limited to 10MB to manage server resources
- 3D preview requires WebGL support (graceful fallback for unsupported browsers)
- Text input limited to prevent performance issues with very long strings

---

## Out of Scope

- Print file generation (CMYK conversion, bleed addition, production files)
- Inventory management for base products
- Fulfillment/shipping integration beyond WooCommerce standard
- Design template marketplace or community sharing
- Social sharing of designs before purchase
- Collaborative design (multiple users editing same design)
- AR preview (view product in real environment)
- Bulk/wholesale ordering interface
- Design approval workflow
- Multi-language support (future enhancement)
