# Design System: WooCommerce Product Customizer

**Style**: Bold & Colorful
**Priority**: Mobile-First
**Date**: 2026-02-03

---

## Brand Color Palette

### Primary Colors

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   PRIMARY          SECONDARY        ACCENT                  │
│   ┌─────────┐     ┌─────────┐     ┌─────────┐              │
│   │         │     │         │     │         │              │
│   │ #FF6B35 │     │ #7C3AED │     │ #06B6D4 │              │
│   │         │     │         │     │         │              │
│   │ Vibrant │     │Electric │     │  Cyan   │              │
│   │ Orange  │     │ Purple  │     │         │              │
│   └─────────┘     └─────────┘     └─────────┘              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Neon Colors (for customizer)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   PINK         BLUE         GREEN        RED          YELLOW       WHITE    │
│   ┌──────┐    ┌──────┐    ┌──────┐    ┌──────┐    ┌──────┐    ┌──────┐   │
│   │      │    │      │    │      │    │      │    │      │    │      │   │
│   │ ●●●  │    │ ●●●  │    │ ●●●  │    │ ●●●  │    │ ●●●  │    │ ●●●  │   │
│   │      │    │      │    │      │    │      │    │      │    │      │   │
│   └──────┘    └──────┘    └──────┘    └──────┘    └──────┘    └──────┘   │
│   #FF6B9D     #00D4FF     #39FF14     #FF3366     #FFFF00     #FFFFFF    │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Surface Colors (Dark Theme for Customizers)

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   DARK           CARD           ELEVATED       BORDER       │
│   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐    │
│   │░░░░░░░░░│   │▒▒▒▒▒▒▒▒▒│   │▓▓▓▓▓▓▓▓▓│   │─────────│    │
│   │░░░░░░░░░│   │▒▒▒▒▒▒▒▒▒│   │▓▓▓▓▓▓▓▓▓│   │         │    │
│   │░░░░░░░░░│   │▒▒▒▒▒▒▒▒▒│   │▓▓▓▓▓▓▓▓▓│   │─────────│    │
│   └─────────┘   └─────────┘   └─────────┘   └─────────┘    │
│    #0A0A0F       #1A1A2E       #252542      rgba(255,      │
│                                              255,255,0.1)   │
└─────────────────────────────────────────────────────────────┘
```

### Semantic Colors

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   SUCCESS        WARNING        ERROR                       │
│   ┌─────────┐   ┌─────────┐   ┌─────────┐                  │
│   │    ✓    │   │    ⚠    │   │    ✕    │                  │
│   │         │   │         │   │         │                  │
│   └─────────┘   └─────────┘   └─────────┘                  │
│    #10B981       #F59E0B       #EF4444                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Typography

### Font Stack

```css
--font-sans: system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
--font-display: 'Inter', system-ui, sans-serif;
```

### Neon Display Fonts

| Font | Use Case | Google Font |
|------|----------|-------------|
| Pacifico | Script/Cursive | `@import url('fonts.google.com/pacifico')` |
| Monoton | Retro/Outline | `@import url('fonts.google.com/monoton')` |
| Bungee | Block/Bold | `@import url('fonts.google.com/bungee')` |
| Sacramento | Elegant | `@import url('fonts.google.com/sacramento')` |

### Type Scale

| Name | Size | Line Height | Weight | Use |
|------|------|-------------|--------|-----|
| xs | 0.75rem (12px) | 1.5 | 400 | Captions, hints |
| sm | 0.875rem (14px) | 1.5 | 400 | Body small |
| base | 1rem (16px) | 1.5 | 400 | Body default |
| lg | 1.125rem (18px) | 1.5 | 500 | Body large |
| xl | 1.25rem (20px) | 1.4 | 600 | Subheadings |
| 2xl | 1.5rem (24px) | 1.3 | 700 | Headings |
| 3xl | 2rem (32px) | 1.2 | 700 | Large headings |
| 4xl | 2.5rem (40px) | 1.1 | 800 | Hero text |

---

## Spacing System

```
┌──────────────────────────────────────────────────────────────────┐
│  SPACING SCALE (rem)                                             │
│                                                                  │
│  xs   sm   md   lg   xl   2xl  3xl                              │
│  ├─┤  ├──┤ ├────┤ ├──────┤ ├────────┤ ├──────────┤ ├──────────┤│
│  4px  8px  16px   24px      32px        48px          64px       │
│  0.25 0.5  1      1.5       2           3             4          │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Border Radius

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  sm (4px)      md (8px)       lg (12px)      xl (16px)   full   │
│  ┌────────┐    ┌────────┐     ┌────────┐     ┌────────┐   ●     │
│  │        │    │        │     │        │     │        │         │
│  └────────┘    └────────┘     └────────┘     └────────┘         │
│                                                                  │
│  Inputs        Cards          Buttons        Modals      Pills  │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Shadows

```css
/* Elevation levels */
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
--shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);

/* Glow effects (for neon) */
--glow-subtle: 0 0 10px var(--color), 0 0 20px var(--color);
--glow-medium: 0 0 10px var(--color), 0 0 20px var(--color), 0 0 40px var(--color);
--glow-intense: 0 0 10px var(--color), 0 0 20px var(--color), 0 0 40px var(--color), 0 0 80px var(--color);
```

---

## Component Library

### Buttons

```
┌──────────────────────────────────────────────────────────────────┐
│  PRIMARY                    SECONDARY                   GHOST    │
│  ┌──────────────────┐      ┌──────────────────┐      ┌────────┐ │
│  │   Add to Cart    │      │     Cancel       │      │  More  │ │
│  └──────────────────┘      └──────────────────┘      └────────┘ │
│  bg: #FF6B35               bg: transparent           bg: trans  │
│  text: white               border: #7C3AED           text: #fff │
│  hover: #FF8C5A            text: #7C3AED             hover: bg  │
│                                                                  │
│  DISABLED                                                        │
│  ┌──────────────────┐                                           │
│  │   Add to Cart    │                                           │
│  └──────────────────┘                                           │
│  bg: #252542                                                     │
│  text: #71717A                                                   │
└──────────────────────────────────────────────────────────────────┘
```

### Inputs

```
┌──────────────────────────────────────────────────────────────────┐
│  DEFAULT                                                         │
│  ┌────────────────────────────────────────────────────────┐     │
│  │ Your text here...                                      │     │
│  └────────────────────────────────────────────────────────┘     │
│  bg: #252542  border: rgba(255,255,255,0.1)                     │
│                                                                  │
│  FOCUS                                                           │
│  ┌────────────────────────────────────────────────────────┐     │
│  │ Your text here                                    15/25│     │
│  └────────────────────────────────────────────────────────┘     │
│  border: #FF6B35  ring: rgba(255,107,53,0.2)                    │
│                                                                  │
│  ERROR                                                           │
│  ┌────────────────────────────────────────────────────────┐     │
│  │ Too long text here...                             26/25│     │
│  └────────────────────────────────────────────────────────┘     │
│  border: #EF4444  ring: rgba(239,68,68,0.2)                     │
│  ⚠ Maximum 25 characters allowed                                │
└──────────────────────────────────────────────────────────────────┘
```

### Color Swatches

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  DEFAULT           HOVER              SELECTED                   │
│     ●                ●                   ●                       │
│   40x40            44x44              44x44 + glow               │
│   no border        scale(1.1)         white border               │
│                                       checkmark                  │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Radio Cards (Size Selector)

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  DEFAULT                                                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ○  Medium          75cm                          $80    │   │
│  └──────────────────────────────────────────────────────────┘   │
│  bg: #252542  border: subtle                                    │
│                                                                  │
│  HOVER                                                           │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ○  Medium          75cm                          $80    │   │
│  └──────────────────────────────────────────────────────────┘   │
│  border: #FF6B35                                                │
│                                                                  │
│  SELECTED                                                        │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  ●  Medium          75cm                          $80    │   │
│  └──────────────────────────────────────────────────────────┘   │
│  border: #FF6B35  bg: rgba(255,107,53,0.1)                      │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Tabs (Mobile)

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  ┌────────┬────────┬────────┬────────┐                          │
│  │  TEXT  │ COLOR  │ STYLE  │  SIZE  │                          │
│  │   ●    │        │        │        │  ← active indicator      │
│  │ ═════  │        │        │        │  ← bottom border         │
│  └────────┴────────┴────────┴────────┘                          │
│                                                                  │
│  Default: text-secondary                                         │
│  Active: text-primary + orange underline                        │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Layout Patterns

### Mobile Layout (Primary)

```
┌─────────────────────────────┐
│        HEADER (60px)        │  ← sticky
├─────────────────────────────┤
│                             │
│      PREVIEW (40vh)         │  ← sticky below header
│                             │
├─────────────────────────────┤
│   TAB BAR                   │  ← sticky below preview
├─────────────────────────────┤
│                             │
│      TAB CONTENT            │  ← scrollable
│      (flexible)             │
│                             │
├─────────────────────────────┤
│  PRICE      [ADD TO CART]   │  ← fixed bottom
└─────────────────────────────┘
```

### Desktop Layout

```
┌─────────────────────────────────────────────────────────────────┐
│                          HEADER                                  │
├─────────────────────────────────────┬───────────────────────────┤
│                                     │                           │
│                                     │    CONTROLS PANEL         │
│         PREVIEW                     │    ┌───────────────────┐  │
│         (sticky)                    │    │ Text Input        │  │
│                                     │    ├───────────────────┤  │
│                                     │    │ Color Picker      │  │
│                                     │    ├───────────────────┤  │
│                                     │    │ Font Selector     │  │
│                                     │    ├───────────────────┤  │
│                                     │    │ Size Selector     │  │
│                                     │    ├───────────────────┤  │
│   BACKGROUND SELECTOR               │    │ Price + CTA       │  │
│                                     │    └───────────────────┘  │
└─────────────────────────────────────┴───────────────────────────┘
```

---

## Breakpoints

| Name | Min Width | Target |
|------|-----------|--------|
| xs | 0 | Small phones |
| sm | 480px | Large phones |
| md | 768px | Tablets |
| lg | 1024px | Small laptops |
| xl | 1280px | Desktops |
| 2xl | 1536px | Large screens |

---

## Animation & Motion

### Timing Functions

```css
--ease-out: cubic-bezier(0.25, 0.46, 0.45, 0.94);
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
--spring: cubic-bezier(0.68, -0.6, 0.32, 1.6);
```

### Durations

| Type | Duration | Use |
|------|----------|-----|
| Instant | 50ms | Micro-interactions |
| Fast | 150ms | Buttons, toggles |
| Normal | 250ms | Modals, panels |
| Slow | 400ms | Page transitions |

### Neon Flicker Animation

```css
@keyframes neon-flicker {
  0%, 19%, 21%, 23%, 25%, 54%, 56%, 100% {
    opacity: 1;
  }
  20%, 24%, 55% {
    opacity: 0.4;
  }
}
```

---

## Accessibility

### Focus States

All interactive elements must have visible focus:

```css
:focus-visible {
  outline: 2px solid var(--primary);
  outline-offset: 2px;
}
```

### Touch Targets

- Minimum 44x44px on mobile
- Minimum 48x48px for primary actions
- 8px minimum spacing between targets

### Color Contrast

- Text on dark: minimum 4.5:1 (AA)
- Decorative neon effects: exempt (visual only)
- Error/success states: 4.5:1 minimum

---

## File Structure

```
assets/
├── css/
│   ├── design-system/
│   │   ├── _variables.css      # All CSS custom properties
│   │   ├── _typography.css     # Font imports & type scale
│   │   ├── _colors.css         # Color palette
│   │   ├── _spacing.css        # Spacing utilities
│   │   └── _animations.css     # Keyframes & transitions
│   │
│   ├── components/
│   │   ├── _buttons.css
│   │   ├── _inputs.css
│   │   ├── _swatches.css
│   │   ├── _tabs.css
│   │   ├── _cards.css
│   │   └── _sliders.css
│   │
│   ├── customizers/
│   │   ├── _neon-base.css      # Neon-specific styles
│   │   ├── _card-base.css      # Card-specific styles
│   │   └── _merch-base.css     # Merchandise styles
│   │
│   └── main.css                 # Main entry point
│
└── fonts/
    └── neon/
        ├── Pacifico.woff2
        ├── Monoton.woff2
        ├── Bungee.woff2
        └── Sacramento.woff2
```
