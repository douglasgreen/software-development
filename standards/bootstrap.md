# Bootstrap Standards & Guidelines for LLM Code Generation

## Core Principles

When generating HTML/CSS code using Bootstrap, always adhere to these standards for consistency, accessibility, and responsiveness.

## 1. Bootstrap Version & Setup

**Always use Bootstrap 5.3+ unless otherwise requested**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
  <!-- Content -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## 2. Class Naming Convention

- **Use Bootstrap utility classes** for spacing, colors, typography, display
- **Add custom classes** (following OOCSS) for component-specific styling
- **Prefix custom classes** to avoid conflicts: `.custom-card`, `.app-header`

```html
<!-- ✓ CORRECT: Bootstrap utilities + custom OOCSS classes -->
<div class="card custom-card shadow-sm">
  <div class="card-body">
    <h2 class="card-title custom-card-title mb-3">Title</h2>
    <p class="card-text text-muted">Content</p>
  </div>
</div>

<!-- ✗ INCORRECT: Inline styles or BEM notation -->
<div class="card" style="margin-bottom: 20px;">
  <h2 class="card__title">Title</h2>
</div>
```

## 3. Grid System Standards

**Always use mobile-first approach with Bootstrap's 12-column grid**

### Responsive Breakpoints
```
xs: <576px (default, no infix)
sm: ≥576px, md: ≥768px, lg: ≥992px, xl: ≥1200px, xxl: ≥1400px
```

```html
<!-- ✓ CORRECT: Mobile-first progression -->
<div class="container">
  <div class="row g-3 g-md-4">
    <div class="col-12 col-md-6 col-lg-4">Content</div>
    <div class="col-12 col-md-6 col-lg-4">Content</div>
    <div class="col-12 col-md-6 col-lg-4">Content</div>
  </div>
</div>

<!-- Container types -->
<div class="container">      <!-- Fixed-width responsive (PREFERRED) -->
<div class="container-fluid"> <!-- Full-width with padding -->
<div class="container-md">    <!-- Full-width until medium breakpoint -->
```

## 4. Utility Classes

**Prefer Bootstrap utilities over custom CSS**

### Spacing
```html
<!-- m/p-{side}-{breakpoint}-{size} where size: 0-5, auto -->
<div class="mb-3 mb-md-4">        <!-- Margin bottom -->
<div class="p-3 px-md-4 py-md-5"> <!-- Padding -->
```

### Display & Layout
```html
<div class="d-none d-md-block">                           <!-- Responsive visibility -->
<div class="d-flex justify-content-between align-items-center"> <!-- Flexbox -->
<div class="d-flex flex-column flex-md-row gap-3">       <!-- Responsive flex direction -->
```

### Typography
```html
<p class="fs-1 fw-bold text-center text-md-start">Text</p>
<p class="text-primary text-muted text-uppercase">Styled text</p>
```

### Colors & Backgrounds
```html
<div class="bg-primary text-white p-3">Primary background</div>
<div class="bg-opacity-75 border border-2 border-primary rounded">Styled</div>
```

## 5. Key Components

### Buttons
```html
<button class="btn btn-primary btn-lg">Button</button>
<button class="btn btn-outline-secondary btn-sm">Outline</button>
<div class="d-grid gap-2">
  <button class="btn btn-primary">Block Button</button>
</div>
```

### Cards
```html
<div class="card h-100"> <!-- h-100 for equal height in grids -->
  <img src="image.jpg" class="card-img-top" alt="Description">
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text">Content</p>
    <a href="#" class="btn btn-primary">Action</a>
  </div>
</div>
```

### Navigation
```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Brand</a>
    <button class="navbar-toggler" type="button" 
            data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

### Modals
```html
<!-- Trigger -->
<button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#myModal">
  Launch Modal
</button>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">Content</div>
      <div class="modal-footer">
        <button class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button class="btn btn-primary">Save</button>
      </div>
    </div>
  </div>
</div>
```

### Forms
```html
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email" 
           aria-describedby="emailHelp" required>
    <div id="emailHelp" class="form-text">Help text here</div>
  </div>
  
  <div class="mb-3">
    <select class="form-select" required>
      <option value="">Choose...</option>
      <option value="1">Option 1</option>
    </select>
  </div>
  
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="check">
    <label class="form-check-label" for="check">Check me</label>
  </div>
  
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

## 6. Accessibility Standards

**Always include proper ARIA attributes and semantic HTML**

```html
<!-- ARIA labels for interactive components -->
<button class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>

<!-- Current page indicator -->
<a class="nav-link active" aria-current="page" href="#">Home</a>

<!-- Form help text association -->
<input type="email" id="email" aria-describedby="emailHelp">
<div id="emailHelp" class="form-text">Help text</div>

<!-- Screen reader only content -->
<span class="visually-hidden">Loading...</span>

<!-- Skip to main content -->
<a href="#main-content" class="visually-hidden-focusable">Skip to main content</a>

<!-- Semantic HTML with Bootstrap -->
<header class="navbar navbar-expand-lg"></header>
<nav aria-label="Main navigation"></nav>
<main id="main-content"></main>
<footer class="bg-dark text-white py-4"></footer>
```

### Color Contrast
```html
<!-- ✓ GOOD: Use Bootstrap's semantic combinations -->
<div class="bg-dark text-white p-3">High contrast</div>
<div class="alert alert-danger">Built-in contrast</div>
<p class="text-body">Regular text</p>
<p class="text-muted">Muted but readable</p>
```

## 7. Customization

### CSS Custom Properties
```css
/* Override Bootstrap variables */
:root {
  --bs-primary: #0066cc;
  --bs-border-radius: 0.375rem;
  --bs-body-font-size: 1rem;
}

/* Custom component using Bootstrap variables and OOCSS */
.custom-panel {
  padding: var(--bs-spacer-3);
  background-color: var(--bs-light);
  border: 1px solid var(--bs-border-color);
  border-radius: var(--bs-border-radius);
}

.custom-panel-title {
  color: var(--bs-primary);
  font-size: var(--bs-font-size-lg);
  margin-bottom: var(--bs-spacer-2);
}
```

### Combining Bootstrap with Custom Classes (OOCSS)
```html
<div class="card custom-product-card shadow-sm">
  <img src="product.jpg" class="card-img-top custom-product-image" alt="Product">
  <div class="card-body">
    <h5 class="card-title custom-product-title">Product</h5>
    <p class="card-text text-muted">Description</p>
    <div class="d-flex justify-content-between align-items-center">
      <span class="fs-4 fw-bold text-primary">$99.99</span>
      <button class="btn btn-primary btn-sm">Add to Cart</button>
    </div>
  </div>
</div>
```

```css
/* Custom CSS using OOCSS principles */
.custom-product-card {
  transition: transform 0.2s ease;
}

.custom-product-card:hover {
  transform: translateY(-4px);
}

.custom-product-image {
  height: 200px;
  object-fit: cover;
}

.custom-product-title {
  font-weight: 600;
  color: var(--bs-gray-900);
}

@media (prefers-reduced-motion: reduce) {
  .custom-product-card {
    transition: none;
  }
}
```

## 8. JavaScript Interactions

**Always use data-bs-* attributes for Bootstrap components**

```html
<!-- Collapse -->
<button class="btn btn-primary" data-bs-toggle="collapse" 
        data-bs-target="#collapseExample">Toggle</button>
<div class="collapse" id="collapseExample">Content</div>

<!-- Dropdown -->
<button class="btn btn-secondary dropdown-toggle" 
        data-bs-toggle="dropdown">Dropdown</button>
<ul class="dropdown-menu">
  <li><a class="dropdown-item" href="#">Action</a></li>
</ul>

<!-- Tooltip (requires initialization) -->
<button data-bs-toggle="tooltip" data-bs-title="Tooltip text">Hover</button>
<script>
  const tooltips = [...document.querySelectorAll('[data-bs-toggle="tooltip"]')]
    .map(el => new bootstrap.Tooltip(el));
</script>
```

## 9. Responsive Patterns

### Images
```html
<img src="image.jpg" class="img-fluid" alt="Description">
<div class="ratio ratio-16x9">
  <img src="image.jpg" alt="Description">
</div>
```

### Visibility
```html
<div class="d-block d-md-none">Mobile only</div>
<div class="d-none d-md-block">Desktop only</div>
<div class="text-center text-md-start p-2 p-md-3 p-lg-5">Responsive spacing</div>
```

### Layout Example
```html
<div class="container">
  <div class="row">
    <div class="col-12 col-lg-8 mb-4 mb-lg-0">
      <article>Main content</article>
    </div>
    <aside class="col-12 col-lg-4">Sidebar</aside>
  </div>
</div>
```

## 10. Common Patterns

### Accordion
```html
<div class="accordion" id="accordionExample">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" data-bs-toggle="collapse" 
              data-bs-target="#collapseOne">Item #1</button>
    </h2>
    <div id="collapseOne" class="accordion-collapse collapse show" 
         data-bs-parent="#accordionExample">
      <div class="accordion-body">Content</div>
    </div>
  </div>
</div>
```

### Alerts
```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Warning!</strong> Check this.
  <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
```

### Badges & Progress
```html
<span class="badge bg-primary">New</span>
<button class="btn btn-primary position-relative">
  Inbox
  <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
    99+<span class="visually-hidden">unread messages</span>
  </span>
</button>

<div class="progress" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">
  <div class="progress-bar" style="width: 75%">75%</div>
</div>
```

## Output Checklist

Before providing Bootstrap code, verify:
- [ ] Bootstrap 5.3+ CDN links included
- [ ] Mobile-first responsive classes (col-12, col-md-6, etc.)
- [ ] Semantic HTML with Bootstrap classes
- [ ] ARIA attributes for interactive components
- [ ] data-bs-* attributes for JavaScript components
- [ ] Utility classes preferred over custom CSS
- [ ] Custom classes follow OOCSS naming (no BEM)
- [ ] Focus states and keyboard navigation supported
- [ ] Color contrast meets accessibility standards
- [ ] Container/row/col structure correct

## Integration Principles

1. **Use Bootstrap utilities first**, add custom classes only when needed
2. **Custom classes complement Bootstrap** using OOCSS principles
3. **Maintain mobile-first approach** throughout
4. **Accessibility standards apply universally**
5. **CSS custom properties work with Bootstrap variables** for theming
6. **Minimize custom CSS** - leverage Bootstrap's comprehensive utility system
