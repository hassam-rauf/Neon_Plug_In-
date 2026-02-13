# Quickstart Guide: WooCommerce Product Customizer

**Feature**: 001-woo-product-customizer
**Date**: 2026-02-03

---

## Prerequisites

- WordPress 6.0+
- WooCommerce 8.0+
- PHP 8.0+
- Node.js 18+ (for development/build)
- Modern browser with WebGL support

---

## Installation

### 1. Clone Repository

```bash
git clone <repository-url>
cd Visual
git checkout 001-woo-product-customizer
```

### 2. Install Development Dependencies

```bash
# PHP dependencies (if using Composer)
cd woo-product-customizer
composer install

# JavaScript dependencies
npm install
```

### 3. Build Assets

```bash
# Development build (with sourcemaps)
npm run dev

# Production build (minified)
npm run build

# Watch mode for development
npm run watch
```

### 4. Install Plugin

Option A: Symlink (Development)
```bash
# Windows (PowerShell as Admin)
New-Item -ItemType SymbolicLink -Path "C:\path\to\wordpress\wp-content\plugins\woo-product-customizer" -Target "C:\path\to\Visual\woo-product-customizer"

# Linux/Mac
ln -s /path/to/Visual/woo-product-customizer /path/to/wordpress/wp-content/plugins/
```

Option B: Copy (Production)
```bash
cp -r woo-product-customizer /path/to/wordpress/wp-content/plugins/
```

### 5. Activate Plugin

1. Go to WordPress Admin → Plugins
2. Find "WooCommerce Product Customizer"
3. Click "Activate"

---

## Development Environment

### Local WordPress Setup

Recommended: Use Local by Flywheel, XAMPP, or Docker

**Docker Compose Example**:
```yaml
version: '3.8'
services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DEBUG: 1
    volumes:
      - ./wordpress:/var/www/html
      - ./woo-product-customizer:/var/www/html/wp-content/plugins/woo-product-customizer
  db:
    image: mysql:8.0
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
      MYSQL_ROOT_PASSWORD: root
```

### Enable Debug Mode

Add to `wp-config.php`:
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);
```

---

## Project Structure

```
woo-product-customizer/
├── woo-product-customizer.php    # Main plugin entry
├── includes/                      # PHP classes
├── assets/
│   ├── js/                        # JavaScript source
│   ├── css/                       # Stylesheets
│   └── models/                    # 3D models (GLB)
├── templates/                     # PHP templates
├── tests/                         # Test suites
├── package.json                   # Node dependencies
└── composer.json                  # PHP dependencies
```

---

## Running Tests

### PHP Unit Tests

```bash
# Install PHPUnit
composer require --dev phpunit/phpunit

# Run tests
./vendor/bin/phpunit

# Run specific test file
./vendor/bin/phpunit tests/phpunit/unit/test-price-calculator.php
```

### JavaScript Tests

```bash
# Run Jest tests
npm test

# Watch mode
npm run test:watch

# Coverage report
npm run test:coverage
```

### E2E Tests (Cypress)

```bash
# Open Cypress UI
npm run cypress:open

# Run headless
npm run cypress:run
```

---

## Creating a Test Product

### Via WP-CLI

```bash
wp wc product create \
  --name="Custom Mug" \
  --type="simple" \
  --regular_price="25.00" \
  --user=1

# Get product ID from output, then:
wp post meta update <PRODUCT_ID> _wpc_enabled "yes"
wp post meta update <PRODUCT_ID> _wpc_type "mug_3zone"
```

### Via Admin UI

1. Products → Add New
2. Enter product name and price
3. Scroll to "Product Customizer" meta box
4. Check "Enable Customizer"
5. Select customizer type (e.g., "Mug (3-Zone)")
6. Configure zones and pricing
7. Publish product

---

## API Testing

### Using cURL

```bash
# Get product config
curl -X GET "http://localhost:8080/wp-json/wpc/v1/config/123"

# Calculate price
curl -X POST "http://localhost:8080/wp-json/wpc/v1/price" \
  -H "Content-Type: application/json" \
  -d '{"product_id": 123, "quantity": 1}'

# Upload image (requires nonce)
curl -X POST "http://localhost:8080/wp-json/wpc/v1/upload" \
  -H "X-WP-Nonce: <nonce>" \
  -F "file=@/path/to/image.jpg" \
  -F "product_id=123" \
  -F "zone_id=front"
```

### Using Postman

Import the OpenAPI spec from `specs/001-woo-product-customizer/contracts/rest-api.yaml`

---

## Development Workflow

### 1. Feature Development

```bash
# Create feature branch
git checkout -b feature/my-feature

# Make changes
# ...

# Run tests
npm test
./vendor/bin/phpunit

# Commit
git add .
git commit -m "feat: add my feature"
```

### 2. Code Style

```bash
# PHP (WordPress Coding Standards)
./vendor/bin/phpcs --standard=WordPress woo-product-customizer/

# JavaScript (ESLint)
npm run lint

# Fix auto-fixable issues
npm run lint:fix
```

### 3. Building for Production

```bash
# Build optimized assets
npm run build

# Create distributable ZIP
npm run package
# Output: dist/woo-product-customizer.zip
```

---

## Common Tasks

### Add a New Product Type

1. Create customizer class:
   ```bash
   touch includes/customizers/class-wpc-newtype-customizer.php
   ```

2. Extend base class:
   ```php
   class WPC_NewType_Customizer extends WPC_Base_Customizer {
       public function get_type(): string {
           return 'newtype';
       }

       public function get_zones(): array {
           return [
               ['id' => 'front', 'label' => 'Front', ...]
           ];
       }
   }
   ```

3. Register in loader:
   ```php
   // In class-wpc-loader.php
   $this->customizers['newtype'] = new WPC_NewType_Customizer();
   ```

4. Create frontend JavaScript:
   ```bash
   touch assets/js/customizer/customizers/newtype.js
   ```

### Add a New 3D Model

1. Export model as GLB (Blender recommended)
2. Ensure UV mapping matches zone definitions
3. Place in `assets/models/`
4. Update product type configuration

### Debug 3D Preview Issues

```javascript
// In browser console on product page
Alpine.store('customizer').debug = true;

// Check Three.js scene
window.wpcThreeScene.children
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| 3D preview blank | Check browser console for WebGL errors; verify model URL |
| Upload fails | Check file size (<10MB), file type (JPEG/PNG/PDF), PHP upload limits |
| Price not updating | Verify AJAX endpoint, check nonce validity |
| Styles not loading | Clear cache, verify CSS enqueue priority |
| Cart data missing | Check session storage, verify add-to-cart hook |

---

## Resources

- [WooCommerce REST API Docs](https://woocommerce.github.io/woocommerce-rest-api-docs/)
- [Three.js Documentation](https://threejs.org/docs/)
- [Fabric.js Documentation](http://fabricjs.com/docs/)
- [Alpine.js Documentation](https://alpinejs.dev/start-here)
- [WordPress Plugin Handbook](https://developer.wordpress.org/plugins/)

---

## Support

- GitHub Issues: [Repository Issues Page]
- Specification: `specs/001-woo-product-customizer/spec.md`
- Architecture: `specs/001-woo-product-customizer/plan.md`
