# Bootstrap Standards & Guidelines for LLM Code Generation

## Core Principles

When generating HTML/CSS code using Bootstrap, always adhere to the following standards:

### 1. Bootstrap Version & Setup

**Always specify Bootstrap 5.3+ unless otherwise requested**

```html
<!-- Standard Bootstrap 5.3 setup -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

  <!-- Custom CSS (if needed) -->
  <link href="styles.css" rel="stylesheet">
</head>
<body>

  <!-- Content -->

  <!-- Bootstrap JS Bundle (includes Popper) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

### 2. Class Naming Convention

**Combine Bootstrap utilities with custom classes when needed:**

- Use **Bootstrap utility classes** for spacing, colors, typography, display, etc.
- Add **custom classes** (following BEM) for component-specific styling
- Prefix custom classes to avoid conflicts: `.custom-card`, `.app-header`

**✓ CORRECT:**
```html
<div class="card custom-card shadow-sm">
  <div class="card-body">
    <h2 class="card-title custom-card__title mb-3">Title</h2>
    <p class="card-text text-muted">Content</p>
  </div>
</div>
```

**✗ INCORRECT:**
```html
<!-- Don't override Bootstrap classes directly -->
<div class="card" style="margin-bottom: 20px;">
  <div class="card-body">
    <h2>Title</h2>
  </div>
</div>
```

### 3. Grid System Standards

**Always use Bootstrap's grid system for layouts:**

#### Container Usage
```html
<!-- Full-width container -->
<div class="container-fluid">
  <!-- Content spans full viewport width with padding -->
</div>

<!-- Fixed-width responsive container (PREFERRED for most content) -->
<div class="container">
  <!-- Content has max-width breakpoints -->
</div>

<!-- Specific breakpoint containers -->
<div class="container-md">
  <!-- Full-width until medium breakpoint -->
</div>
```

#### Grid Structure
```html
<!-- Basic grid -->
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Full width mobile, half on tablet, third on desktop -->
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Content -->
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Content -->
    </div>
  </div>
</div>

<!-- Grid with gutters (spacing between columns) -->
<div class="container">
  <div class="row g-3 g-md-4">
    <!-- g-3 = gap of 1rem, g-md-4 = gap of 1.5rem on md+ -->
    <div class="col-12 col-sm-6 col-lg-3">Content</div>
    <div class="col-12 col-sm-6 col-lg-3">Content</div>
    <div class="col-12 col-sm-6 col-lg-3">Content</div>
    <div class="col-12 col-sm-6 col-lg-3">Content</div>
  </div>
</div>

<!-- No gutters -->
<div class="row g-0">
  <!-- Columns touch each other -->
</div>
```

#### Responsive Breakpoints
```
xs: <576px (default, no infix)
sm: ≥576px
md: ≥768px
lg: ≥992px
xl: ≥1200px
xxl: ≥1400px
```

**Always use mobile-first approach:**
```html
<!-- ✓ CORRECT: Mobile first, progressively enhanced -->
<div class="col-12 col-md-6 col-xl-4">

<!-- ✗ INCORRECT: Desktop first -->
<div class="col-xl-4 col-md-6 col-12">
```

## 4. Utility Classes

### Spacing Utilities
**Use Bootstrap spacing utilities instead of custom margins/padding:**

```html
<!-- Margin: m-{size}, mt-{size}, mb-{size}, ms-{size}, me-{size}, mx-{size}, my-{size} -->
<!-- Padding: p-{size}, pt-{size}, pb-{size}, ps-{size}, pe-{size}, px-{size}, py-{size} -->
<!-- Sizes: 0, 1 (0.25rem), 2 (0.5rem), 3 (1rem), 4 (1.5rem), 5 (3rem), auto -->

<div class="mb-3 mb-md-4">
  <!-- Bottom margin: 1rem on mobile, 1.5rem on md+ -->
</div>

<div class="p-3 px-md-4 py-md-5">
  <!-- Padding: 1rem all sides mobile, 1.5rem x-axis and 3rem y-axis on md+ -->
</div>

<div class="mt-auto">
  <!-- Pushes element to bottom in flex container -->
</div>
```

### Display Utilities
```html
<!-- Display -->
<div class="d-none d-md-block">
  <!-- Hidden on mobile, visible on md+ -->
</div>

<div class="d-block d-lg-none">
  <!-- Visible up to lg, hidden on lg+ -->
</div>

<!-- Flexbox -->
<div class="d-flex justify-content-between align-items-center">
  <!-- Flex container with space-between and vertical center -->
</div>

<div class="d-flex flex-column flex-md-row gap-3">
  <!-- Column on mobile, row on md+, with gap -->
</div>

<!-- Grid -->
<div class="d-grid gap-2">
  <!-- CSS Grid with gap -->
  <button class="btn btn-primary">Button 1</button>
  <button class="btn btn-secondary">Button 2</button>
</div>
```

### Typography Utilities
```html
<!-- Font sizes -->
<p class="fs-1">Display text (largest)</p>
<p class="fs-6">Small text (smallest)</p>

<!-- Font weight -->
<p class="fw-light">Light text (300)</p>
<p class="fw-normal">Normal text (400)</p>
<p class="fw-bold">Bold text (700)</p>

<!-- Text alignment -->
<p class="text-start text-md-center">
  <!-- Left aligned on mobile, centered on md+ -->
</p>

<!-- Text transform -->
<p class="text-uppercase">Uppercase text</p>
<p class="text-capitalize">Capitalized Text</p>

<!-- Text colors -->
<p class="text-primary">Primary color text</p>
<p class="text-muted">Muted text</p>
<p class="text-body-secondary">Secondary body text</p>
```

### Color & Background Utilities
```html
<!-- Background colors -->
<div class="bg-primary text-white p-3">Primary background</div>
<div class="bg-light text-dark p-3">Light background</div>
<div class="bg-body-secondary p-3">Secondary background</div>

<!-- Opacity -->
<div class="bg-primary bg-opacity-75">75% opacity background</div>

<!-- Borders -->
<div class="border border-2 border-primary rounded">
  <!-- 2px primary border with rounded corners -->
</div>

<div class="border-top border-bottom">
  <!-- Only top and bottom borders -->
</div>
```

## 5. Components

### Buttons
```html
<!-- Basic buttons -->
<button type="button" class="btn btn-primary">Primary Button</button>
<button type="button" class="btn btn-secondary">Secondary Button</button>
<button type="button" class="btn btn-outline-primary">Outline Button</button>

<!-- Sizes -->
<button class="btn btn-primary btn-lg">Large Button</button>
<button class="btn btn-primary">Default Button</button>
<button class="btn btn-primary btn-sm">Small Button</button>

<!-- Block buttons (full width) -->
<div class="d-grid gap-2">
  <button class="btn btn-primary">Block Button</button>
  <button class="btn btn-secondary">Block Button</button>
</div>

<!-- Button states -->
<button class="btn btn-primary" disabled>Disabled Button</button>
<button class="btn btn-primary active" aria-pressed="true">Active Button</button>

<!-- Button group -->
<div class="btn-group" role="group" aria-label="Basic button group">
  <button type="button" class="btn btn-outline-primary">Left</button>
  <button type="button" class="btn btn-outline-primary">Middle</button>
  <button type="button" class="btn btn-outline-primary">Right</button>
</div>
```

### Cards
```html
<!-- Basic card -->
<div class="card">
  <div class="card-body">
    <h5 class="card-title">Card Title</h5>
    <p class="card-text">Card content goes here.</p>
    <a href="#" class="btn btn-primary">Action</a>
  </div>
</div>

<!-- Card with image -->
<div class="card">
  <img src="image.jpg" class="card-img-top" alt="Description">
  <div class="card-body">
    <h5 class="card-title">Card Title</h5>
    <p class="card-text">Some quick example text.</p>
  </div>
  <div class="card-footer text-muted">
    2 days ago
  </div>
</div>

<!-- Card grid -->
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  <div class="col">
    <div class="card h-100">
      <div class="card-body">
        <h5 class="card-title">Card 1</h5>
        <p class="card-text">Content</p>
      </div>
    </div>
  </div>
  <div class="col">
    <div class="card h-100">
      <div class="card-body">
        <h5 class="card-title">Card 2</h5>
        <p class="card-text">Content</p>
      </div>
    </div>
  </div>
  <div class="col">
    <div class="card h-100">
      <div class="card-body">
        <h5 class="card-title">Card 3</h5>
        <p class="card-text">Content</p>
      </div>
    </div>
  </div>
</div>
```

### Navigation
```html
<!-- Navbar (responsive with mobile toggle) -->
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Brand</a>

    <!-- Mobile toggle button -->
    <button class="navbar-toggler" type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarNav"
            aria-controls="navbarNav"
            aria-expanded="false"
            aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <!-- Collapsible content -->
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Features</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Pricing</a>
        </li>
      </ul>
    </div>
  </div>
</nav>

<!-- Tabs -->
<ul class="nav nav-tabs" role="tablist">
  <li class="nav-item" role="presentation">
    <button class="nav-link active" id="home-tab"
            data-bs-toggle="tab" data-bs-target="#home"
            type="button" role="tab"
            aria-controls="home" aria-selected="true">
      Home
    </button>
  </li>
  <li class="nav-item" role="presentation">
    <button class="nav-link" id="profile-tab"
            data-bs-toggle="tab" data-bs-target="#profile"
            type="button" role="tab"
            aria-controls="profile" aria-selected="false">
      Profile
    </button>
  </li>
</ul>

<div class="tab-content" id="myTabContent">
  <div class="tab-pane fade show active" id="home"
       role="tabpanel" aria-labelledby="home-tab">
    Home content
  </div>
  <div class="tab-pane fade" id="profile"
       role="tabpanel" aria-labelledby="profile-tab">
    Profile content
  </div>
</div>
```

### Modals
```html
<!-- Modal trigger -->
<button type="button" class="btn btn-primary"
        data-bs-toggle="modal" data-bs-target="#exampleModal">
  Launch Modal
</button>

<!-- Modal structure -->
<div class="modal fade" id="exampleModal" tabindex="-1"
     aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal Title</h5>
        <button type="button" class="btn-close"
                data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        Modal content goes here.
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary"
                data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>

<!-- Responsive modal sizes -->
<div class="modal-dialog modal-sm">Small modal</div>
<div class="modal-dialog">Default modal</div>
<div class="modal-dialog modal-lg">Large modal</div>
<div class="modal-dialog modal-xl">Extra large modal</div>
<div class="modal-dialog modal-fullscreen-md-down">
  <!-- Full screen below md breakpoint -->
</div>
```

### Alerts
```html
<!-- Basic alerts -->
<div class="alert alert-primary" role="alert">
  A simple primary alert—check it out!
</div>

<div class="alert alert-danger" role="alert">
  An error occurred!
</div>

<!-- Dismissible alert -->
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Warning!</strong> You should check this.
  <button type="button" class="btn-close"
          data-bs-dismiss="alert" aria-label="Close"></button>
</div>

<!-- Alert with icon (using Bootstrap Icons) -->
<div class="alert alert-success d-flex align-items-center" role="alert">
  <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img"
       aria-label="Success:">
    <use xlink:href="#check-circle-fill"/>
  </svg>
  <div>Operation completed successfully!</div>
</div>
```

## 6. Forms

### Form Structure
```html
<!-- Basic form -->
<form>
  <!-- Text input -->
  <div class="mb-3">
    <label for="email" class="form-label">Email address</label>
    <input type="email" class="form-control" id="email"
           aria-describedby="emailHelp" required>
    <div id="emailHelp" class="form-text">
      We'll never share your email with anyone else.
    </div>
  </div>

  <!-- Password input -->
  <div class="mb-3">
    <label for="password" class="form-label">Password</label>
    <input type="password" class="form-control" id="password" required>
  </div>

  <!-- Checkbox -->
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="remember">
    <label class="form-check-label" for="remember">
      Remember me
    </label>
  </div>

  <!-- Submit button -->
  <button type="submit" class="btn btn-primary">Submit</button>
</form>

<!-- Form validation states -->
<div class="mb-3">
  <label for="validInput" class="form-label">Valid input</label>
  <input type="text" class="form-control is-valid"
         id="validInput" value="Valid value" required>
  <div class="valid-feedback">
    Looks good!
  </div>
</div>

<div class="mb-3">
  <label for="invalidInput" class="form-label">Invalid input</label>
  <input type="text" class="form-control is-invalid"
         id="invalidInput" required>
  <div class="invalid-feedback">
    Please provide a valid value.
  </div>
</div>

<!-- Select dropdown -->
<div class="mb-3">
  <label for="country" class="form-label">Country</label>
  <select class="form-select" id="country" required>
    <option value="">Choose...</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="ca">Canada</option>
  </select>
</div>

<!-- Textarea -->
<div class="mb-3">
  <label for="message" class="form-label">Message</label>
  <textarea class="form-control" id="message" rows="3"></textarea>
</div>

<!-- Radio buttons -->
<fieldset class="mb-3">
  <legend class="form-label">Choose an option</legend>
  <div class="form-check">
    <input class="form-check-input" type="radio"
           name="options" id="option1" value="1" checked>
    <label class="form-check-label" for="option1">
      Option 1
    </label>
  </div>
  <div class="form-check">
    <input class="form-check-input" type="radio"
           name="options" id="option2" value="2">
    <label class="form-check-label" for="option2">
      Option 2
    </label>
  </div>
</fieldset>
```

### Form Layouts
```html
<!-- Horizontal form -->
<form>
  <div class="row mb-3">
    <label for="inputEmail" class="col-sm-2 col-form-label">Email</label>
    <div class="col-sm-10">
      <input type="email" class="form-control" id="inputEmail">
    </div>
  </div>

  <div class="row mb-3">
    <label for="inputPassword" class="col-sm-2 col-form-label">Password</label>
    <div class="col-sm-10">
      <input type="password" class="form-control" id="inputPassword">
    </div>
  </div>

  <button type="submit" class="btn btn-primary">Sign in</button>
</form>

<!-- Inline form -->
<form class="row row-cols-lg-auto g-3 align-items-center">
  <div class="col-12">
    <label class="visually-hidden" for="inlineFormInputGroupUsername">
      Username
    </label>
    <div class="input-group">
      <div class="input-group-text">@</div>
      <input type="text" class="form-control"
             id="inlineFormInputGroupUsername" placeholder="Username">
    </div>
  </div>

  <div class="col-12">
    <button type="submit" class="btn btn-primary">Submit</button>
  </div>
</form>
```

## 7. Accessibility Standards

### Always Include Proper ARIA Attributes
```html
<!-- Interactive components need aria labels -->
<button class="btn-close" data-bs-dismiss="modal"
        aria-label="Close"></button>

<!-- Use aria-current for active navigation items -->
<li class="nav-item">
  <a class="nav-link active" aria-current="page" href="#">Home</a>
</li>

<!-- Use aria-describedby for form help text -->
<input type="email" class="form-control" id="email"
       aria-describedby="emailHelp">
<div id="emailHelp" class="form-text">Help text here</div>

<!-- Hidden content for screen readers -->
<span class="visually-hidden">Loading...</span>

<!-- Skip to main content link -->
<a href="#main-content" class="visually-hidden-focusable">
  Skip to main content
</a>
```

### Focus Management
```html
<!-- Ensure focus is visible (Bootstrap handles this by default) -->
<button class="btn btn-primary">
  <!-- Bootstrap applies focus-visible styles automatically -->
</button>

<!-- For custom focus styles, use Bootstrap's focus utilities -->
<div class="custom-element" tabindex="0">
  <!-- Add in custom CSS: -->
  <!-- .custom-element:focus-visible { outline: 2px solid var(--bs-primary); } -->
</div>
```

### Color Contrast
```html
<!-- ✓ GOOD: Use Bootstrap's semantic color combinations -->
<div class="bg-dark text-white p-3">High contrast text</div>
<div class="alert alert-danger">Error message (built-in contrast)</div>

<!-- ✗ BAD: Custom color combinations without checking contrast -->
<div class="bg-warning text-light p-3">Poor contrast</div>

<!-- ✓ GOOD: Use text-body, text-muted for proper contrast -->
<p class="text-body">Regular body text</p>
<p class="text-muted">Muted but still readable</p>
```

### Semantic HTML with Bootstrap
```html
<!-- Use semantic HTML elements with Bootstrap classes -->
<header class="navbar navbar-expand-lg">
  <!-- Header content -->
</header>

<nav aria-label="Main navigation">
  <ul class="nav">
    <!-- Navigation items -->
  </ul>
</nav>

<main id="main-content">
  <article class="card">
    <div class="card-body">
      <h2 class="card-title">Article Title</h2>
      <p class="card-text">Article content</p>
    </div>
  </article>
</main>

<footer class="bg-dark text-white py-4">
  <!-- Footer content -->
</footer>
```

## 8. Customization with CSS Variables

### Using Bootstrap's CSS Custom Properties
```css
/* Override Bootstrap variables in your custom CSS */
:root {
  /* Brand colors */
  --bs-primary: #0066cc;
  --bs-secondary: #6c757d;
  --bs-success: #28a745;
  --bs-danger: #dc3545;

  /* Spacing */
  --bs-gutter-x: 1.5rem;

  /* Typography */
  --bs-body-font-size: 1rem;
  --bs-body-line-height: 1.6;

  /* Border radius */
  --bs-border-radius: 0.375rem;
  --bs-border-radius-lg: 0.5rem;
}

/* Custom component using Bootstrap variables */
.custom-panel {
  padding: var(--bs-spacer-3);
  background-color: var(--bs-light);
  border: 1px solid var(--bs-border-color);
  border-radius: var(--bs-border-radius);
}

.custom-panel__title {
  color: var(--bs-primary);
  font-size: var(--bs-font-size-lg);
  margin-bottom: var(--bs-spacer-2);
}
```

### Adding Custom Classes Alongside Bootstrap
```html
<!-- Combine Bootstrap utilities with custom classes -->
<div class="card custom-product-card shadow-sm">
  <img src="product.jpg" class="card-img-top custom-product-card__image"
       alt="Product name">
  <div class="card-body">
    <h5 class="card-title custom-product-card__title">Product Name</h5>
    <p class="card-text text-muted mb-3">Description</p>
    <div class="d-flex justify-content-between align-items-center">
      <span class="fs-4 fw-bold text-primary">$99.99</span>
      <button class="btn btn-primary btn-sm">Add to Cart</button>
    </div>
  </div>
</div>
```

```css
/* Custom CSS for the component */
.custom-product-card {
  transition: transform 0.2s ease;
}

.custom-product-card:hover {
  transform: translateY(-4px);
}

.custom-product-card__image {
  height: 200px;
  object-fit: cover;
}

.custom-product-card__title {
  font-weight: 600;
  color: var(--bs-gray-900);
}

@media (prefers-reduced-motion: reduce) {
  .custom-product-card {
    transition: none;
  }
}
```

## 9. Responsive Design Patterns

### Responsive Images
```html
<!-- Image that scales with container -->
<img src="image.jpg" class="img-fluid" alt="Description">

<!-- Responsive image with different aspect ratios -->
<div class="ratio ratio-16x9">
  <img src="image.jpg" alt="Description">
</div>

<!-- Different ratios available -->
<div class="ratio ratio-1x1">1:1 Square</div>
<div class="ratio ratio-4x3">4:3</div>
<div class="ratio ratio-16x9">16:9 Widescreen</div>
<div class="ratio ratio-21x9">21:9 Ultra-wide</div>

<!-- Rounded images -->
<img src="avatar.jpg" class="rounded-circle" alt="Avatar"
     style="width: 100px; height: 100px; object-fit: cover;">
```

### Responsive Typography
```html
<!-- Display headings (larger, responsive by default) -->
<h1 class="display-1">Display 1</h1>
<h2 class="display-2">Display 2</h2>
<h3 class="display-3">Display 3</h3>

<!-- Responsive font sizes -->
<p class="fs-1 fs-md-2 fs-lg-3">
  <!-- Larger on mobile, smaller on bigger screens -->
</p>

<!-- Lead paragraph -->
<p class="lead">
  Make a paragraph stand out with larger, lighter text.
</p>
```

### Responsive Visibility
```html
<!-- Show/hide at different breakpoints -->
<div class="d-block d-md-none">
  <!-- Visible only on mobile -->
  <nav class="navbar">Mobile Navigation</nav>
</div>

<div class="d-none d-md-block">
  <!-- Hidden on mobile, visible on md+ -->
  <nav class="navbar">Desktop Navigation</nav>
</div>

<!-- Responsive spacing -->
<div class="p-2 p-md-3 p-lg-5">
  <!-- Less padding on mobile, more on larger screens -->
</div>

<!-- Responsive text alignment -->
<div class="text-center text-md-start">
  <!-- Centered on mobile, left-aligned on md+ -->
</div>
```

### Responsive Containers
```html
<!-- Stacked on mobile, side-by-side on larger screens -->
<div class="container">
  <div class="row">
    <div class="col-12 col-lg-8">
      <article class="mb-4 mb-lg-0">
        <!-- Main content -->
      </article>
    </div>
    <aside class="col-12 col-lg-4">
      <!-- Sidebar -->
    </aside>
  </div>
</div>

<!-- Card deck that responds to screen size -->
<div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 g-4">
  <div class="col">
    <div class="card h-100">Card 1</div>
  </div>
  <div class="col">
    <div class="card h-100">Card 2</div>
  </div>
  <div class="col">
    <div class="card h-100">Card 3</div>
  </div>
  <div class="col">
    <div class="card h-100">Card 4</div>
  </div>
</div>
```

## 10. Common Page Layouts

### Hero Section
```html
<section class="hero bg-primary text-white py-5">
  <div class="container">
    <div class="row align-items-center min-vh-50">
      <div class="col-12 col-lg-6">
        <h1 class="display-3 fw-bold mb-3">Welcome to Our Site</h1>
        <p class="lead mb-4">
          A compelling description that explains what you offer.
        </p>
        <div class="d-grid gap-2 d-sm-flex">
          <button class="btn btn-light btn-lg">Get Started</button>
          <button class="btn btn-outline-light btn-lg">Learn More</button>
        </div>
      </div>
      <div class="col-12 col-lg-6 mt-4 mt-lg-0">
        <img src="hero-image.jpg" class="img-fluid rounded" alt="Hero image">
      </div>
    </div>
  </div>
</section>
```

### Feature Section
```html
<section class="features py-5">
  <div class="container">
    <h2 class="text-center mb-5">Our Features</h2>
    <div class="row g-4">
      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 border-0 shadow-sm">
          <div class="card-body text-center">
            <div class="feature-icon bg-primary bg-opacity-10 rounded-circle
                        d-inline-flex align-items-center justify-content-center
                        mb-3" style="width: 80px; height: 80px;">
              <!-- Icon here -->
              <svg class="text-primary" width="32" height="32">
                <!-- SVG content -->
              </svg>
            </div>
            <h3 class="h5 mb-3">Feature One</h3>
            <p class="text-muted">
              Description of the first feature and its benefits.
            </p>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 border-0 shadow-sm">
          <div class="card-body text-center">
            <div class="feature-icon bg-success bg-opacity-10 rounded-circle
                        d-inline-flex align-items-center justify-content-center
                        mb-3" style="width: 80px; height: 80px;">
              <!-- Icon here -->
            </div>
            <h3 class="h5 mb-3">Feature Two</h3>
            <p class="text-muted">
              Description of the second feature and its benefits.
            </p>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 border-0 shadow-sm">
          <div class="card-body text-center">
            <div class="feature-icon bg-info bg-opacity-10 rounded-circle
                        d-inline-flex align-items-center justify-content-center
                        mb-3" style="width: 80px; height: 80px;">
              <!-- Icon here -->
            </div>
            <h3 class="h5 mb-3">Feature Three</h3>
            <p class="text-muted">
              Description of the third feature and its benefits.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

### Dashboard Layout
```html
<div class="container-fluid">
  <div class="row">
    <!-- Sidebar -->
    <nav class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse"
         id="sidebarMenu">
      <div class="position-sticky pt-3">
        <ul class="nav flex-column">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">
              Dashboard
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Orders</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Products</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Customers</a>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Main content -->
    <main class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
      <div class="d-flex justify-content-between flex-wrap flex-md-nowrap
                  align-items-center pt-3 pb-2 mb-3 border-bottom">
        <h1 class="h2">Dashboard</h1>
        <button class="btn btn-sm btn-outline-secondary">
          Export
        </button>
      </div>

      <!-- Dashboard content -->
      <div class="row g-3 mb-4">
        <div class="col-12 col-sm-6 col-xl-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-muted mb-2">Total Sales</h5>
              <p class="h3 mb-0">$24,500</p>
            </div>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-xl-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-muted mb-2">New Orders</h5>
              <p class="h3 mb-0">156</p>
            </div>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-xl-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-muted mb-2">Customers</h5>
              <p class="h3 mb-0">1,234</p>
            </div>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-xl-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-muted mb-2">Avg. Order</h5>
              <p class="h3 mb-0">$157</p>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</div>
```

### Pricing Table
```html
<section class="pricing py-5">
  <div class="container">
    <h2 class="text-center mb-5">Choose Your Plan</h2>
    <div class="row g-4 justify-content-center">
      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100">
          <div class="card-body d-flex flex-column">
            <h3 class="card-title text-center">Basic</h3>
            <p class="text-center text-muted">For individuals</p>
            <div class="text-center my-4">
              <span class="display-4 fw-bold">$9</span>
              <span class="text-muted">/month</span>
            </div>
            <ul class="list-unstyled mb-4">
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Feature one
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Feature two
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Feature three
              </li>
            </ul>
            <button class="btn btn-outline-primary mt-auto">
              Get Started
            </button>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 border-primary shadow">
          <div class="card-body d-flex flex-column">
            <div class="badge bg-primary position-absolute top-0 end-0 m-3">
              Popular
            </div>
            <h3 class="card-title text-center">Pro</h3>
            <p class="text-center text-muted">For teams</p>
            <div class="text-center my-4">
              <span class="display-4 fw-bold">$29</span>
              <span class="text-muted">/month</span>
            </div>
            <ul class="list-unstyled mb-4">
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                All Basic features
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Advanced feature
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Priority support
              </li>
            </ul>
            <button class="btn btn-primary mt-auto">
              Get Started
            </button>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100">
          <div class="card-body d-flex flex-column">
            <h3 class="card-title text-center">Enterprise</h3>
            <p class="text-center text-muted">For organizations</p>
            <div class="text-center my-4">
              <span class="display-4 fw-bold">$99</span>
              <span class="text-muted">/month</span>
            </div>
            <ul class="list-unstyled mb-4">
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                All Pro features
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Custom integrations
              </li>
              <li class="mb-2">
                <svg class="text-success me-2" width="16" height="16">
                  <use xlink:href="#check"/>
                </svg>
                Dedicated support
              </li>
            </ul>
            <button class="btn btn-outline-primary mt-auto">
              Contact Sales
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

### Footer
```html
<footer class="bg-dark text-white py-5">
  <div class="container">
    <div class="row g-4">
      <div class="col-12 col-md-6 col-lg-3">
        <h5 class="mb-3">Company</h5>
        <ul class="list-unstyled">
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">About Us</a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">Careers</a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">Press</a>
          </li>
        </ul>
      </div>

      <div class="col-12 col-md-6 col-lg-3">
        <h5 class="mb-3">Products</h5>
        <ul class="list-unstyled">
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">Features</a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">Pricing</a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">
              Documentation
            </a>
          </li>
        </ul>
      </div>

      <div class="col-12 col-md-6 col-lg-3">
        <h5 class="mb-3">Support</h5>
        <ul class="list-unstyled">
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">
              Help Center
            </a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">Contact</a>
          </li>
          <li class="mb-2">
            <a href="#" class="text-white-50 text-decoration-none">FAQ</a>
          </li>
        </ul>
      </div>

      <div class="col-12 col-md-6 col-lg-3">
        <h5 class="mb-3">Newsletter</h5>
        <p class="text-white-50">Stay updated with our latest news.</p>
        <form class="mt-3">
          <div class="input-group">
            <input type="email" class="form-control"
                   placeholder="Your email"
                   aria-label="Email address">
            <button class="btn btn-primary" type="submit">
              Subscribe
            </button>
          </div>
        </form>
      </div>
    </div>

    <hr class="my-4 bg-white opacity-25">

    <div class="row">
      <div class="col-12 col-md-6 text-center text-md-start">
        <p class="mb-0 text-white-50">
          © 2024 Company Name. All rights reserved.
        </p>
      </div>
      <div class="col-12 col-md-6 text-center text-md-end mt-3 mt-md-0">
        <a href="#" class="text-white-50 text-decoration-none me-3">
          Privacy Policy
        </a>
        <a href="#" class="text-white-50 text-decoration-none">
          Terms of Service
        </a>
      </div>
    </div>
  </div>
</footer>
```

## 11. Performance & Best Practices

### Loading Bootstrap Efficiently
```html
<!-- Load CSS in <head> -->
<link rel="preconnect" href="https://cdn.jsdelivr.net">
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN"
      crossorigin="anonymous">

<!-- Load JS before closing </body> -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL"
        crossorigin="anonymous">
</script>
```

### Minimize Custom CSS
```html
<!-- ✓ GOOD: Use Bootstrap utilities -->
<div class="d-flex justify-content-between align-items-center p-3 bg-light">
  Content
</div>

<!-- ✗ AVOID: Writing custom CSS when Bootstrap utilities exist -->
<div class="custom-flex-container">
  Content
</div>
<style>
.custom-flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #f8f9fa;
}
</style>
```

### Avoid Overriding Bootstrap Unnecessarily
```css
/* ✓ GOOD: Extend Bootstrap with custom classes */
.custom-card-hover {
  transition: transform 0.2s ease;
}

.custom-card-hover:hover {
  transform: translateY(-4px);
}

/* ✗ AVOID: Overriding Bootstrap classes directly */
.card {
  /* This affects ALL cards globally */
  border: 3px solid red;
}

/* ✓ BETTER: Use modifier classes */
.card.card--custom {
  border: 3px solid red;
}
```

## 12. JavaScript Interactions

### Data Attributes for Components
```html
<!-- Always use data-bs-* attributes for Bootstrap components -->

<!-- Collapse -->
<button class="btn btn-primary" type="button"
        data-bs-toggle="collapse"
        data-bs-target="#collapseExample"
        aria-expanded="false"
        aria-controls="collapseExample">
  Toggle Collapse
</button>
<div class="collapse" id="collapseExample">
  <div class="card card-body">
    Collapsible content
  </div>
</div>

<!-- Dropdown -->
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button"
          data-bs-toggle="dropdown"
          aria-expanded="false">
    Dropdown
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
    <li><hr class="dropdown-divider"></li>
    <li><a class="dropdown-item" href="#">Separated link</a></li>
  </ul>
</div>

<!-- Tooltip (requires initialization) -->
<button type="button" class="btn btn-secondary"
        data-bs-toggle="tooltip"
        data-bs-placement="top"
        data-bs-title="Tooltip text">
  Hover for tooltip
</button>

<!-- Initialize tooltips in JavaScript -->
<script>
  const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
  const tooltipList = [...tooltipTriggerList].map(
    tooltipTriggerEl => new bootstrap.Tooltip(tooltipTriggerEl)
  );
</script>

<!-- Popover -->
<button type="button" class="btn btn-danger"
        data-bs-toggle="popover"
        data-bs-title="Popover title"
        data-bs-content="Popover content here">
  Click for popover
</button>

<script>
  const popoverTriggerList = document.querySelectorAll('[data-bs-toggle="popover"]');
  const popoverList = [...popoverTriggerList].map(
    popoverTriggerEl => new bootstrap.Popover(popoverTriggerEl)
  );
</script>
```

### Programmatic API Usage
```javascript
// Working with modals programmatically
const myModal = new bootstrap.Modal(document.getElementById('myModal'), {
  keyboard: false,
  backdrop: 'static'
});

myModal.show();
myModal.hide();

// Event listeners
const myModalEl = document.getElementById('myModal');
myModalEl.addEventListener('shown.bs.modal', () => {
  console.log('Modal is now visible');
});

// Toast notifications
const toastTrigger = document.getElementById('liveToastBtn');
const toastLiveExample = document.getElementById('liveToast');

if (toastTrigger) {
  toastTrigger.addEventListener('click', () => {
    const toast = new bootstrap.Toast(toastLiveExample);
    toast.show();
  });
}
```

## 13. Common Patterns Reference

### Breadcrumbs
```html
<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item"><a href="#">Library</a></li>
    <li class="breadcrumb-item active" aria-current="page">Data</li>
  </ol>
</nav>
```

### Pagination
```html
<nav aria-label="Page navigation">
  <ul class="pagination justify-content-center">
    <li class="page-item disabled">
      <a class="page-link" href="#" aria-label="Previous">
        <span aria-hidden="true">&laquo;</span>
      </a>
    </li>
    <li class="page-item active" aria-current="page">
      <a class="page-link" href="#">1</a>
    </li>
    <li class="page-item"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item">
      <a class="page-link" href="#" aria-label="Next">
        <span aria-hidden="true">&raquo;</span>
      </a>
    </li>
  </ul>
</nav>
```

### Badge
```html
<h1>
  Example heading
  <span class="badge bg-secondary">New</span>
</h1>

<button type="button" class="btn btn-primary position-relative">
  Inbox
  <span class="position-absolute top-0 start-100 translate-middle badge
               rounded-pill bg-danger">
    99+
    <span class="visually-hidden">unread messages</span>
  </span>
</button>
```

### Progress Bar
```html
<div class="progress" role="progressbar"
     aria-label="Basic example"
     aria-valuenow="75"
     aria-valuemin="0"
     aria-valuemax="100">
  <div class="progress-bar" style="width: 75%"></div>
</div>

<!-- With label -->
<div class="progress" role="progressbar"
     aria-label="Example with label"
     aria-valuenow="25"
     aria-valuemin="0"
     aria-valuemax="100">
  <div class="progress-bar" style="width: 25%">25%</div>
</div>

<!-- Multiple bars -->
<div class="progress">
  <div class="progress-bar" style="width: 15%"></div>
  <div class="progress-bar bg-success" style="width: 30%"></div>
  <div class="progress-bar bg-info" style="width: 20%"></div>
</div>
```

### Spinner
```html
<!-- Border spinner -->
<div class="spinner-border" role="status">
  <span class="visually-hidden">Loading...</span>
</div>

<!-- Growing spinner -->
<div class="spinner-grow text-primary" role="status">
  <span class="visually-hidden">Loading...</span>
</div>

<!-- Button with spinner -->
<button class="btn btn-primary" type="button" disabled>
  <span class="spinner-border spinner-border-sm me-2"
        role="status"
        aria-hidden="true"></span>
  Loading...
</button>
```

### Toast Notification
```html
<div class="toast-container position-fixed bottom-0 end-0 p-3">
  <div id="liveToast" class="toast" role="alert"
       aria-live="assertive" aria-atomic="true">
    <div class="toast-header">
      <strong class="me-auto">Notification</strong>
      <small>Just now</small>
      <button type="button" class="btn-close"
              data-bs-dismiss="toast"
              aria-label="Close"></button>
    </div>
    <div class="toast-body">
      Hello, this is a toast message!
    </div>
  </div>
</div>
```

### Accordion
```html
<div class="accordion" id="accordionExample">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" type="button"
              data-bs-toggle="collapse"
              data-bs-target="#collapseOne"
              aria-expanded="true"
              aria-controls="collapseOne">
        Accordion Item #1
      </button>
    </h2>
    <div id="collapseOne" class="accordion-collapse collapse show"
         data-bs-parent="#accordionExample">
      <div class="accordion-body">
        Content for first item.
      </div>
    </div>
  </div>

  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" type="button"
              data-bs-toggle="collapse"
              data-bs-target="#collapseTwo"
              aria-expanded="false"
              aria-controls="collapseTwo">
        Accordion Item #2
      </button>
    </h2>
    <div id="collapseTwo" class="accordion-collapse collapse"
         data-bs-parent="#accordionExample">
      <div class="accordion-body">
        Content for second item.
      </div>
    </div>
  </div>
</div>
```

---

## Output Checklist

Before providing Bootstrap code, verify:
- [ ] Bootstrap 5.3+ CDN links included (or version specified)
- [ ] Mobile-first responsive classes used (col-12, col-md-6, etc.)
- [ ] Proper semantic HTML with Bootstrap classes
- [ ] ARIA attributes included for interactive components
- [ ] data-bs-* attributes used correctly for JavaScript components
- [ ] Utility classes preferred over custom CSS when available
- [ ] Custom classes follow BEM naming (custom-component__element)
- [ ] Focus states and keyboard navigation supported
- [ ] Color contrast meets accessibility standards
- [ ] Responsive breakpoints appropriately applied
- [ ] Container/row/col structure used correctly
- [ ] Component-specific requirements met (modals need IDs, tooltips need initialization, etc.)

---

## Integration with CSS Standards

When Bootstrap is available, follow these principles to maintain consistency with your CSS standards:

1. **Use Bootstrap utilities first**, add custom classes only when needed
2. **Custom classes should complement Bootstrap**, not override it
3. **Follow BEM naming for custom additions**: `.custom-card__header--featured`
4. **Maintain mobile-first approach** consistent across both frameworks
5. **Accessibility standards apply equally** whether using Bootstrap or custom CSS
6. **CSS custom properties work alongside Bootstrap variables** for theming

**Example of proper integration:**
```html
<div class="card custom-product-card shadow-sm mb-4">
  <img src="product.jpg" class="card-img-top custom-product-card__image"
       alt="Product">
  <div class="card-body">
    <h5 class="card-title custom-product-card__title mb-3">
      Product Name
    </h5>
    <p class="card-text text-muted">Description here</p>
    <div class="d-flex justify-content-between align-items-center mt-auto">
      <span class="fs-4 fw-bold text-primary">$99.99</span>
      <button class="btn btn-primary">Add to Cart</button>
    </div>
  </div>
</div>
```

```css
/* Custom CSS complementing Bootstrap */
.custom-product-card {
  transition: transform var(--bs-transition-duration) ease;
}

.custom-product-card:hover {
  transform: translateY(-4px);
}

.custom-product-card__image {
  height: 250px;
  object-fit: cover;
}

.custom-product-card__title {
  color: var(--bs-gray-900);
  font-weight: 600;
}

@media (prefers-reduced-motion: reduce) {
  .custom-product-card {
    transition: none;
  }
}
```
