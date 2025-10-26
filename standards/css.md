# CSS Standards & Guidelines for LLM Code Generation

## Core Principles

When generating CSS code, always adhere to the following standards:

### 1. Selector Structure
- **ALWAYS use class or ID selectors as top-level selectors** - never use bare element selectors at the root level
- Prefer class selectors (`.class-name`) over ID selectors (`#id-name`) for styling
- Use IDs only for unique, single-instance components or JavaScript hooks
- Nest element selectors only within class/ID contexts

**✓ CORRECT:**
```css
.card {
  padding: 1rem;
}

.card h2 {
  font-size: 1.5rem;
}
```

**✗ INCORRECT:**
```css
h2 {
  font-size: 1.5rem;
}

div {
  padding: 1rem;
}
```

### 2. Naming Conventions
- Use **lowercase with hyphens** (kebab-case): `.nav-menu`, `.btn-primary`
- Use **OOCSS methodology** for composable components:
  - Base objects: `.card`, `.btn`, `.media`
  - Skin classes: `.primary`, `.secondary`, `.featured`
  - Layout classes: `.box`, `.container`, `.row`
  - State classes: `.is-active`, `.is-disabled`, `.is-open`
- Prefix utility classes with `u-`: `.u-text-center`, `.u-hidden`
- Prefix JavaScript hooks with `js-`: `.js-toggle`, `.js-modal-trigger`
- Prefix state classes with `is-` or `has-`: `.is-active`, `.has-error`

### 3. Object-Oriented CSS Structure

**Separate structure from skin** and **container from content**:

```css
/* STRUCTURE: Base object with layout/positioning */
.box {
  display: flex;
  padding: 1rem;
  margin-bottom: 1rem;
}

/* SKIN: Visual themes applied to objects */
.primary {
  background-color: #007bff;
  color: #ffffff;
  border-radius: 0.25rem;
}

.secondary {
  background-color: #6c757d;
  color: #ffffff;
  border-radius: 0.25rem;
}

/* USAGE: Compose classes */
<div class="box primary">Primary box</div>
<div class="box secondary">Secondary box</div>
```

**Separate container from content:**

```css
/* Container shouldn't dictate child styling */
.card {
  padding: 1.5rem;
  background: #ffffff;
  border-radius: 0.5rem;
}

/* Content objects remain independent */
.heading {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

/* USAGE: Compose independent objects */
<div class="card">
  <h2 class="heading">Title</h2>
</div>
```

**Create reusable objects:**

```css
/* Base media object (reusable layout pattern) */
.media {
  display: flex;
  align-items: flex-start;
}

.media-figure {
  margin-right: 1rem;
  flex-shrink: 0;
}

.media-body {
  flex: 1;
}

/* USAGE: Reuse across different contexts */
<div class="media">
  <div class="media-figure">
    <img src="avatar.jpg" alt="">
  </div>
  <div class="media-body">
    <p>Content here</p>
  </div>
</div>
```

## 4. Responsive Design Standards

### Mobile-First Approach
Always write base styles for mobile, then enhance for larger screens:

```css
.container {
  width: 100%;
  padding: 1rem;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    max-width: 720px;
    margin: 0 auto;
    padding: 1.5rem;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    max-width: 960px;
    padding: 2rem;
  }
}
```

### Standard Breakpoints
```css
/* Mobile: default (no media query) */
/* Tablet: min-width: 768px */
/* Desktop: min-width: 1024px */
/* Large Desktop: min-width: 1280px */
```

### Flexible Units
- Use **rem/em** for font sizes and spacing (scalable)
- Use **%** or **viewport units (vw, vh)** for layouts
- Use **px** only for fixed dimensions (borders, shadows)
- Use **clamp()** for fluid typography:

```css
.heading {
  font-size: clamp(1.5rem, 4vw, 3rem);
}
```

## 5. Accessibility Standards

### Focus States
Always provide visible focus indicators:

```css
.btn {
  padding: 0.75rem 1.5rem;
  border: 2px solid transparent;
  transition: all 0.2s ease;
}

.btn:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}

.btn:focus:not(:focus-visible) {
  outline: none;
}

.btn:focus-visible {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

### Color Contrast
Ensure WCAG AA compliance (4.5:1 for normal text, 3:1 for large text):

```css
.primary {
  color: #ffffff;
  background-color: #0056b3; /* High contrast */
}

.alert.error {
  color: #721c24; /* Dark red text */
  background-color: #f8d7da; /* Light red background */
  border: 1px solid #f5c6cb;
}
```

### Screen Reader Support
```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  overflow: visible;
  clip: auto;
  white-space: normal;
}
```

### Motion Preferences
```css
.animated {
  transition: transform 0.3s ease;
}

@media (prefers-reduced-motion: reduce) {
  .animated {
    transition: none;
  }
}
```

## 6. Organization & File Structure

### Logical Ordering
```css
/* 1. Reset/Base */
.component {
  /* 2. Positioning */
  position: relative;
  z-index: 10;

  /* 3. Box Model */
  display: flex;
  width: 100%;
  padding: 1rem;
  margin-bottom: 1rem;

  /* 4. Typography */
  font-size: 1rem;
  line-height: 1.5;

  /* 5. Visual */
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 0.5rem;

  /* 6. Misc */
  cursor: pointer;
  transition: all 0.2s ease;
}
```

### Component Structure (OOCSS Pattern)
```css
/* ===== Object: Card ===== */

/* Base structure object */
.card {
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Sub-objects for card parts */
.card-header {
  padding: 1.5rem;
}

.card-body {
  padding: 1.5rem;
  flex: 1;
}

.card-footer {
  padding: 1rem 1.5rem;
}

/* ===== Skins (visual themes) ===== */

.elevated {
  background-color: #ffffff;
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.bordered {
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 0.5rem;
}

.featured {
  border: 2px solid #007bff;
}

/* ===== Modifiers (size/spacing variations) ===== */

.compact {
  font-size: 0.875rem;
}

.compact > .card-header,
.compact > .card-body,
.compact > .card-footer {
  padding: 1rem;
}

/* ===== State classes ===== */

.is-highlighted {
  box-shadow: 0 4px 12px rgba(0, 123, 255, 0.2);
}

/* USAGE: Compose classes together */
<div class="card elevated featured">
  <div class="card-header">
    <h2 class="heading">Title</h2>
  </div>
  <div class="card-body">
    <p class="text">Content</p>
  </div>
  <div class="card-footer">
    <button class="btn primary">Action</button>
  </div>
</div>
```

## 7. Common Patterns

### Layout: Flexbox Grid
```css
/* Structure object */
.grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin: 0;
  padding: 0;
  list-style: none;
}

.grid-item {
  flex: 1 1 100%;
  min-width: 0; /* Prevent overflow */
}

/* Size modifiers */
@media (min-width: 768px) {
  .half {
    flex: 1 1 calc(50% - 0.5rem);
  }

  .third {
    flex: 1 1 calc(33.333% - 0.67rem);
  }

  .quarter {
    flex: 1 1 calc(25% - 0.75rem);
  }
}

/* USAGE */
<ul class="grid">
  <li class="grid-item half">Item 1</li>
  <li class="grid-item half">Item 2</li>
</ul>
```

### Layout: CSS Grid
```css
/* Base grid structure */
.grid-layout {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

/* Fixed grid variant */
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 1.5rem;
}

/* Span modifiers */
.span-6 {
  grid-column: span 6;
}

.span-4 {
  grid-column: span 4;
}

.span-3 {
  grid-column: span 3;
}

/* USAGE */
<div class="grid-12">
  <div class="span-6">Half width</div>
  <div class="span-6">Half width</div>
</div>
```

### Buttons
```css
/* Base button structure */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  font-weight: 500;
  line-height: 1;
  text-align: center;
  text-decoration: none;
  border: 2px solid transparent;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.btn:active {
  transform: translateY(0);
}

/* Button skins (visual themes) */
.primary {
  color: #ffffff;
  background-color: #007bff;
  border-color: #007bff;
}

.primary:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

.secondary {
  color: #ffffff;
  background-color: #6c757d;
  border-color: #6c757d;
}

.secondary:hover {
  background-color: #545b62;
  border-color: #545b62;
}

.outline {
  color: #007bff;
  background-color: transparent;
  border-color: #007bff;
}

.outline:hover {
  color: #ffffff;
  background-color: #007bff;
}

/* Size modifiers */
.large {
  padding: 1rem 2rem;
  font-size: 1.125rem;
}

.small {
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
}

/* State classes */
.is-disabled {
  opacity: 0.6;
  cursor: not-allowed;
  pointer-events: none;
}

/* USAGE: Compose classes */
<button class="btn primary large">Large Primary Button</button>
<button class="btn secondary">Secondary Button</button>
<button class="btn outline small">Small Outline Button</button>
<button class="btn primary is-disabled">Disabled Button</button>
```

### Forms
```css
/* Form structure objects */
.form-group {
  margin-bottom: 1.5rem;
}

.form-label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #333333;
}

.form-control {
  display: block;
  width: 100%;
  padding: 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #333333;
  background-color: #ffffff;
  border: 1px solid #cccccc;
  border-radius: 0.375rem;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

.form-control:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

.form-text {
  display: block;
  margin-top: 0.5rem;
  font-size: 0.875rem;
  color: #6c757d;
}

/* State classes for validation */
.has-error .form-control {
  border-color: #dc3545;
}

.has-error .form-control:focus {
  border-color: #dc3545;
  box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
}

.has-error .form-text {
  color: #dc3545;
}

.has-success .form-control {
  border-color: #28a745;
}

.has-success .form-control:focus {
  border-color: #28a745;
  box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.1);
}

/* USAGE: Compose with state classes */
<div class="form-group has-error">
  <label class="form-label" for="email">Email</label>
  <input type="email" id="email" class="form-control">
  <span class="form-text">Please enter a valid email address.</span>
</div>
```

### Media Object Pattern
```css
/* Reusable media object structure */
.media {
  display: flex;
  align-items: flex-start;
}

.media-figure {
  margin-right: 1rem;
  flex-shrink: 0;
}

.media-body {
  flex: 1;
  min-width: 0; /* Prevent overflow */
}

/* Alignment modifiers */
.media.center {
  align-items: center;
}

.media.bottom {
  align-items: flex-end;
}

/* Reverse modifier */
.media.reverse {
  flex-direction: row-reverse;
}

.media.reverse .media-figure {
  margin-right: 0;
  margin-left: 1rem;
}

/* USAGE: Versatile across contexts */
<div class="media">
  <div class="media-figure">
    <img src="avatar.jpg" alt="Avatar" class="avatar">
  </div>
  <div class="media-body">
    <h3 class="heading">Username</h3>
    <p class="text">Message content goes here...</p>
  </div>
</div>
```

### Utility Classes
```css
/* Spacing utilities */
.u-mt-1 { margin-top: 0.5rem; }
.u-mt-2 { margin-top: 1rem; }
.u-mt-3 { margin-top: 1.5rem; }
.u-mb-1 { margin-bottom: 0.5rem; }
.u-mb-2 { margin-bottom: 1rem; }
.u-mb-3 { margin-bottom: 1.5rem; }
.u-p-1 { padding: 0.5rem; }
.u-p-2 { padding: 1rem; }
.u-p-3 { padding: 1.5rem; }

/* Text utilities */
.u-text-center { text-align: center; }
.u-text-right { text-align: right; }
.u-text-bold { font-weight: 700; }
.u-text-uppercase { text-transform: uppercase; }

/* Display utilities */
.u-hidden { display: none; }
.u-block { display: block; }
.u-inline-block { display: inline-block; }
.u-flex { display: flex; }
.u-grid { display: grid; }

/* Responsive visibility */
@media (max-width: 767px) {
  .u-hidden-mobile { display: none; }
}

@media (min-width: 768px) {
  .u-hidden-tablet { display: none; }
}

@media (min-width: 1024px) {
  .u-hidden-desktop { display: none; }
}
```

## 8. Performance & Best Practices

### Avoid Deep Nesting
**Limit to 3 levels maximum:**

```css
/* ✓ GOOD - Flat, composable structure */
.nav { }
.nav-list { }
.nav-item { }
.nav-link { }

/* ✗ BAD - Deep nesting */
.nav .list .item a span {
  /* too specific, hard to override */
}
```

### Favor Composition Over Specificity
```css
/* ✓ GOOD - Low specificity, composable */
.box { }
.elevated { }
.primary { }

/* Usage: <div class="box elevated primary"> */

/* ✗ BAD - High specificity */
.box.box-elevated-primary { }
```

### Use CSS Custom Properties
```css
.theme {
  --color-primary: #007bff;
  --color-secondary: #6c757d;
  --color-success: #28a745;
  --color-danger: #dc3545;

  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;

  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.25rem;

  --border-radius: 0.375rem;
  --transition-speed: 0.2s;
}

.btn.primary {
  padding: var(--spacing-md) var(--spacing-lg);
  background-color: var(--color-primary);
  border-radius: var(--border-radius);
  transition: all var(--transition-speed) ease;
}
```

### Create Reusable Base Objects
```css
/* Base objects that can be extended */
.list-reset {
  margin: 0;
  padding: 0;
  list-style: none;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
}

/* USAGE: Compose into components */
<ul class="list-reset nav-list">
  <li class="nav-item">Item</li>
</ul>
```

## 9. Documentation Template

When providing CSS code, include comments:

```css
/**
 * Object: Navigation Menu
 * Description: Responsive navigation with mobile hamburger menu
 * Dependencies: JavaScript for mobile toggle (.js-nav-toggle)
 *
 * Usage:
 * <nav class="nav">
 *   <ul class="nav-list">
 *     <li class="nav-item is-active">
 *       <a href="#" class="nav-link">Link</a>
 *     </li>
 *   </ul>
 * </nav>
 */

/* Base structure */
.nav {
  /* Base styles */
}

.nav-list {
  /* List reset and layout */
}

.nav-item {
  /* Item positioning */
}

.nav-link {
  /* Link styles */
}

/* State classes */
.nav-item.is-active {
  /* Active state */
}

/* Mobile styles (default) */
@media (max-width: 767px) {
  .nav-list {
    /* Mobile-specific styles */
  }
}

/* Tablet and desktop */
@media (min-width: 768px) {
  .nav-list {
    /* Enhanced styles for larger screens */
  }
}
```

---

## OOCSS Key Principles Summary

### 1. Separate Structure from Skin
```css
/* Structure (layout) */
.box { display: flex; padding: 1rem; }

/* Skin (appearance) */
.primary { background: blue; color: white; }
.secondary { background: gray; color: white; }

/* Compose: <div class="box primary"> */
```

### 2. Separate Container from Content
```css
/* ✓ GOOD - Content is independent */
.card { padding: 1rem; }
.heading { font-size: 1.5rem; }

/* ✗ BAD - Content depends on container */
.card .heading { font-size: 1.5rem; }
```

### 3. Use Composition
```css
/* Multiple small classes composed together */
<button class="btn primary large is-loading">
  Submit
</button>
```

### 4. Create Reusable Objects
```css
/* Objects can be reused anywhere */
.media { display: flex; }
.media-figure { margin-right: 1rem; }
.media-body { flex: 1; }

/* Used in comments, profiles, notifications, etc. */
```

---

## Output Checklist

Before providing CSS code, verify:
- [ ] All top-level selectors are classes or IDs
- [ ] Structure is separated from skin (layout vs. appearance)
- [ ] Container is separated from content (no location-dependent styling)
- [ ] Objects are reusable and composable
- [ ] State classes use `is-` or `has-` prefix
- [ ] Mobile-first responsive design used
- [ ] Focus states included for interactive elements
- [ ] Color contrast meets WCAG AA standards
- [ ] Semantic class names following OOCSS conventions
- [ ] CSS custom properties used for repeated values
- [ ] Transitions respect `prefers-reduced-motion`
- [ ] Code is organized logically with comments
- [ ] Specificity kept as low as practical
- [ ] Flexible units (rem/em/%) used appropriately
- [ ] Classes are small, single-purpose, and composable
