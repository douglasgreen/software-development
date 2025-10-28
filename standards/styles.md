# Style Standards

## Introduction

This document outlines a comprehensive set of CSS standards for developing consistent, accessible, and responsive web applications. These standards are designed to guide developers and AI-powered assistants in creating a harmonious and readable user experience across all projects.

The foundation of these standards is **Bootstrap 5.x**. We leverage its responsive grid system, pre-built components, and extensive utility classes to ensure rapid development and cross-device compatibility. The primary goal is to use Bootstrap's utilities as the default, extending with minimal custom CSS only when necessary.

These standards emphasize:

-   **Consistency**: A unified look and feel through a shared system of colors, spacing, and typography defined in CSS custom properties.
-   **Responsiveness**: A **desktop-first** approach. Designs should be optimized for larger screens and gracefully adapt to smaller viewports (tablet and mobile) using Bootstrap's breakpoints.
-   **Accessibility**: Strict adherence to WCAG 2.1 AA guidelines, including sufficient color contrast, full keyboard navigability, and semantic HTML for screen reader support.
-   **Performance**: Prioritizing a fast user experience by using simple selectors, optimized assets, and minimal animations. We target modern browsers (Chrome 90+, Firefox 88+, Safari 15+, Edge 90+).

## 1. Color Palette (Light Theme)

Our color scheme is designed to be professional, clear, and accessible. All colors must be defined as CSS custom properties (e.g., `--bs-primary`, `--bs-body-color`) for easy maintenance. All text and background color combinations must meet the WCAG AA contrast ratio of at least 4.5:1.

### Primary Palette

-   **Primary (Brand & Interactive Elements)**: A clear, professional blue used for primary actions and interactive elements.
    -   Value: `#0d6efd` (Bootstrap's default blue)
    -   Usage: Primary buttons, links, active form field outlines, key icons.
-   **Secondary (Supporting Elements)**: A neutral gray for less prominent elements.
    -   Value: `#6c757d` (Bootstrap's `gray-600`)
    -   Usage: Secondary buttons, subheadings, metadata text, and decorative borders.

### Semantic Colors

-   **Success**: Green for positive confirmations and successful states.
    -   Value: `#198754` (Bootstrap's `success`)
    -   Usage: Success alerts, validation pass indicators, confirmation messages.
-   **Warning**: Orange for non-critical alerts that require user attention.
    -   Value: `#ffc107` (Bootstrap's `warning`)
    -   Usage: Warning messages, pending statuses, form field suggestions.
-   **Danger**: Red for errors and destructive actions.
    -   Value: `#dc3545` (Bootstrap's `danger`)
    -   Usage: Error alerts, validation fail indicators, delete buttons.
-   **Info**: A light blue for informational hints and asides.
    -   Value: `#0dcaf0` (Bootstrap's `info`)
    -   Usage: Informational callouts, neutral alerts.

### Neutral Grays (Text, Backgrounds, Borders)

-   **Page Background**: `#f8f9fa` (`gray-100`)
-   **Component Background**: `#ffffff` (`white`) for cards, modals, and forms.
-   **Body Text**: `#212529` (Bootstrap's `gray-900`) for maximum readability.
-   **Borders & Dividers**: `#dee2e6` (`gray-300`) for subtle separation.

### Guidelines

-   Use Bootstrap's color utility classes (e.g., `text-primary`, `bg-success`) wherever possible.
-   Interactive elements should have a visually distinct `:hover` and `:focus` state, typically by darkening the primary color by 15% (e.g., `#0d6efd` on hover becomes `#0b5ed7`).

## 2. Typography

Typography must be clear, legible, and hierarchical. We prioritize high-performance system fonts and use a responsive, `rem`-based scale.

### Font Families

-   **Primary (Body & UI)**: Use the system font stack for native performance and feel.
    -   Value: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif`
    -   Usage: All body copy, labels, and general interface text.
-   **Secondary (Headings)**: Optionally, an elegant and readable web font for headings to add brand character.
    -   Example: `'Inter', sans-serif` (loaded via `<link>` with `font-display: swap`).
    -   Usage: `<h1>` through `<h3>` tags or major section titles.

### Font Scale and Weights

All sizes are based on a root font size of `16px`. Use `rem` units for scalability.

-   **Headings**:
    -   `h1`: 2.0rem (32px), `font-weight: 600` (Semibold)
    -   `h2`: 1.75rem (28px), `font-weight: 600`
    -   `h3`: 1.5rem (24px), `font-weight: 600`
    -   `h4`: 1.25rem (20px), `font-weight: 500` (Medium)
-   **Body Text**: 1rem (16px), `font-weight: 400` (Normal).
-   **Labels & Metadata**: 0.875rem (14px), `font-weight: 400`.
-   **Line Height**: `1.5` for all body text to ensure comfortable readability. `1.2` for headings.

### Guidelines

-   Use Bootstrap's typography utilities (e.g., `fw-bold`, `fs-5`, `text-muted`).
-   All text should be left-aligned (`text-start`) for LTR languages.

## 3. Layout and Spacing

We use a desktop-first, responsive layout built on Bootstrap's grid system. Spacing is managed with a consistent, modular scale via Bootstrap's spacing utilities.

### Grid and Structure

-   **Main Content Container**: Use Bootstrap's `.container` or `.container-fluid`. For fixed-width layouts, center the container and apply a `max-width` (e.g., `1200px`) for large desktops.
-   **Page Layout**: Structure layouts with the Bootstrap grid (`.row`, `.col-*`). Design for desktop first (e.g., `.col-lg-8`) and then add smaller breakpoint classes (`.col-md-12`) as needed.
-   **Flexbox**: Use flexbox utilities (`d-flex`, `justify-content-*`, `align-items-*`) for component-level alignment of items in navigation bars, cards, and forms.

### Spacing Scale

Rely on Bootstrap’s spacing utilities (`p-*`, `m-*`, `gap-*`), which are based on a `$spacer` variable of `1rem` (16px) by default.

-   **Micro (0.25rem / 4px)**: `p-1`, `m-1` - Gaps inside small components.
-   **Small (0.5rem / 8px)**: `p-2`, `m-2` - Gaps between icons and text.
-   **Base (1rem / 16px)**: `p-3`, `m-3` - Default padding for components like cards and alerts.
-   **Medium (1.5rem / 24px)**: `p-4`, `m-4` - Separation between larger page sections.
-   **Large (3rem / 48px)**: `p-5`, `m-5` - Margins around the main content container.

### Borders and Shadows

-   **Borders**: Use a `1px solid var(--bs-border-color)` (e.g., `#dee2e6`) for subtle definition on cards, tables, and form inputs.
-   **Border Radius**: Apply a consistent corner radius using Bootstrap's `.rounded` classes (default is `0.375rem`).
-   **Shadows**: Use subtle shadows (`.shadow-sm`) to create depth and elevate interactive elements like modals, dropdowns, and primary cards on hover. Avoid overuse to maintain a clean design.

## 4. Core Components and Interactions

Standardize the appearance and behavior of common UI components.

### Buttons

-   **Primary**: `.btn .btn-primary` for the main call to action on a page.
-   **Secondary**: `.btn .btn-secondary` for less important actions.
-   **States**: Ensure all buttons have clear `:hover`, `:focus`, and `:disabled` states. Focus states must use Bootstrap’s `focus-ring` for accessibility.
-   **Icons**: When using icons in buttons (from **Bootstrap Icons**), ensure they have appropriate padding (`gap-2` in a flex container).

### Forms

-   **Inputs**: Use `.form-control` for all text inputs, textareas, and selects.
-   **Labels**: All inputs must have a corresponding `<label>` with the `.form-label` class for accessibility.
-   **Validation**: Use Bootstrap's validation classes (`.is-invalid`, `.is-valid`) to provide clear feedback, paired with descriptive helper text.

### Cards

-   **Structure**: Use the `.card` component with `.card-body` for all primary content containers. `.card-header` and `.card-footer` can be used for structure.
-   **Styling**: Cards should have a `1px` border, standard border-radius, and use the base padding unit (`p-3`). They may use a subtle box-shadow on hover to indicate interactivity.

### Interactions & Animations

-   **Transitions**: Apply smooth, quick transitions for state changes like hover and focus (`transition: all 0.2s ease-in-out`).
-   **Animations**: Animations should be minimal and purposeful (e.g., fade-in for new content). All animations must be disabled when a user has `prefers-reduced-motion` enabled.

## 5. Accessibility

Accessibility is non-negotiable. All development must follow these principles.

-   **Color Contrast**: Verify all text/background combinations pass WCAG AA standards (4.5:1).
-   **Keyboard Navigation**: All interactive elements (links, buttons, form fields) must be reachable and operable using the Tab key. The focus indicator must always be visible and clear.
-   **ARIA Attributes**: Use ARIA roles and attributes where semantic HTML is insufficient. For example:
    -   `aria-label` for icon-only buttons (e.g., `<button aria-label="Close">`).
    -   `aria-describedby` to associate form inputs with error messages.
    -   `aria-live="polite"` for regions with dynamic content like alerts or status updates, so screen readers announce changes.
-   **Semantic HTML**: Use HTML elements according to their purpose (`<nav>`, `<main>`, `<button>`, etc.). All images must have descriptive `alt` text.
-   **Touch Targets**: Ensure all interactive elements have a minimum touch target size of 44x44 pixels.

## Implementation Notes

-   **Custom CSS**: Write custom CSS only for styles not achievable with Bootstrap utilities. Place custom styles in a separate stylesheet that loads after Bootstrap to ensure proper cascading. Avoid using `!important` except as a last resort.
-   **Icons**: Use the **Bootstrap Icons** library exclusively for consistency and performance. Embed them as inline SVG for scalability and styling control.
