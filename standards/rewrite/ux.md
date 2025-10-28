# Web Application UI Design Standards - System Prompt Extension

## UI/UX Design Standards for Database-Driven Web Applications

### Layout Architecture

**Primary Layout Structure:**
- Use a **three-tier responsive layout system**:
  - **Mobile (< 768px)**: Single column, stacked navigation
  - **Tablet (768px - 1199px)**: Two-column flex layout where appropriate
  - **Desktop (≥ 1200px)**: Multi-column with sidebar(s)

**Page Structure Components:**
1. **Header (Fixed/Sticky)**: 60-80px height
   - Logo/brand (left)
   - Primary navigation (center or right)
   - User menu/profile (far right)
   - Search bar (if applicable)
   - Use `position: sticky; top: 0;` with high z-index

2. **Sidebar(s)**: 
   - **Primary sidebar**: 250-300px wide on desktop, collapsible on mobile
   - Position: Left for navigation, right for contextual actions/filters
   - Should collapse to hamburger menu or slide-in drawer on mobile
   - Use `role="navigation"` or `role="complementary"`

3. **Main Content Area**: 
   - Min-width: 320px (smallest mobile)
   - Max-width: 1200-1400px for readability (center with auto margins)
   - Padding: 15-20px mobile, 30-40px desktop
   - Use `<main role="main">` semantic element

4. **Footer**: 
   - Minimal height, typically 60-100px
   - Copyright, links, version info
   - Should not contain critical navigation

### Navigation Patterns

**Primary Navigation:**
- **Top Navigation Bar**: For 5-7 primary sections
- **Sidebar Navigation**: For 8+ items or hierarchical structures
- **Breadcrumbs**: Always include for pages 2+ levels deep
- **Active states**: Clear visual distinction (bold, different color, border)
- **Mobile**: Hamburger menu icon (☰) in top-right, slides in from left/right

**Navigation Accessibility:**
```html
<nav role="navigation" aria-label="Main navigation">
  <ul class="nav-list">
    <li><a href="#" aria-current="page">Dashboard</a></li>
  </ul>
</nav>
```

### CRUD Operation Patterns

**CREATE Operations:**
1. **Entry Point**: Prominent "+ New [Item]" or "Create" button
   - Position: Top-right of list/table view
   - Color: Primary action color (typically blue/green)
   - Icon: Plus (+) symbol
   
2. **Form Location**: 
   - **Option A**: Modal/dialog overlay (for simple forms, 3-8 fields)
   - **Option B**: Dedicated new page (for complex forms, 9+ fields)
   - **Option C**: Inline expansion/slide-down (for single-field quick adds)
   
3. **Form Progression**:
   - Single-page form for ≤ 12 fields
   - Multi-step wizard for 13+ fields or logical groupings
   - Progress indicator for multi-step (breadcrumb or step numbers)
   - "Save Draft" option for long forms

**READ Operations (Displaying Data):**

1. **List Views**:
   - **Table format**: 5+ data columns, sortable headers
   - **Card/grid format**: Visual/media content, 2-6 key fields
   - **List format**: Mobile-friendly, 2-3 key fields per row
   
2. **Table Standards**:
   - Zebra striping for readability (`nth-child` CSS)
   - Hover states on rows
   - Sortable column headers with arrow indicators
   - Pagination: 25/50/100 per page, show "Showing X-Y of Z results"
   - Sticky header on scroll
   
3. **Detail View**:
   - **Header section**: Title, key metadata, primary actions
   - **Content sections**: Grouped in cards or panels with headings
   - **Action buttons**: Top-right (Edit, Delete) or floating action button
   - **Related data**: Tabs or collapsible sections

**UPDATE Operations:**
1. **Entry Points**:
   - "Edit" button/icon (pencil icon) next to each item
   - Entire row clickable (for list views)
   - Direct field editing (inline editing) for simple text fields
   
2. **Edit Form Layout**:
   - **In-place modal**: Same location as create form
   - **Same-page edit**: Replace view with form (with "Cancel" to revert)
   - Pre-populate all fields with current values
   - Show "Save" and "Cancel" buttons prominently
   
3. **Inline Editing**:
   - Double-click or single-click to edit
   - Field converts to input, auto-focus
   - Save on Enter or blur; Cancel on Escape
   - Show success confirmation (checkmark animation or toast)

**DELETE Operations:**
1. **Delete Triggers**:
   - "Delete" button (red/warning color) with trash icon
   - Position: Bottom of edit form or in action menu (⋮)
   
2. **Confirmation Pattern** (REQUIRED):
   ```
   Modal: "Are you sure you want to delete [Item Name]?"
   - This action cannot be undone.
   [Cancel] [Delete]
   ```
   - Make "Cancel" the default/easy action
   - "Delete" button should be red/warning color
   
3. **Soft Delete Option**: Offer "Archive" instead where appropriate

### Form Design Standards

**Form Structure:**
1. **Field Layout**:
   - Vertical labels (above inputs) - better for responsiveness
   - Full-width inputs on mobile
   - 2-column layout on desktop for short fields (city/state)
   - Logical grouping with `<fieldset>` and `<legend>`

2. **Field Order**:
   - Most important/frequently filled fields first
   - Logical flow (first name → last name → email → phone)
   - Required fields at top, optional at bottom

3. **Input Types**:
   - Use semantic HTML5 inputs: `email`, `tel`, `date`, `number`, `url`
   - Datepickers for dates
   - Dropdowns/select for 3-12 options
   - Radio buttons for 2-4 mutually exclusive options
   - Checkboxes for multiple selections or single boolean
   - Textarea for multi-line text (3+ rows minimum)

**Form Validation:**
1. **Inline Validation**:
   - Show errors below/beside field on blur
   - Green checkmark for valid fields
   - Red border + error message for invalid fields
   - Error message pattern: "[Field] must be [requirement]"
   
2. **Submit Validation**:
   - Disable submit until required fields complete (or show error summary)
   - Scroll to first error on submit
   - Show all errors in a summary box at top of form
   
3. **Accessibility**:
   ```html
   <label for="email">Email *</label>
   <input 
     type="email" 
     id="email" 
     name="email" 
     required 
     aria-required="true"
     aria-describedby="email-error"
   >
   <span id="email-error" class="error" role="alert"></span>
   ```

**Form Actions:**
- Primary action (Save/Submit): Right-aligned, prominent color
- Secondary action (Cancel): Left-aligned or left of primary, subdued
- Destructive action (Delete): Separated, red/warning color
- Button text: Action verbs ("Save Changes", not just "Submit")

### Data Display Components

**Tables:**
```html
<div class="table-responsive">
  <table class="table table-hover" role="table">
    <thead>
      <tr>
        <th scope="col">
          Name 
          <button aria-label="Sort by name">↕</button>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td data-label="Name">Item 1</td>
      </tr>
    </tbody>
  </table>
</div>
```
- Always wrap in `.table-responsive` for mobile
- Use `data-label` attributes for mobile card-style display
- Checkbox column for bulk actions (first column)

**Cards:**
- Use for dashboards, galleries, product listings
- Max-width: 300-400px
- Include: thumbnail, title, 2-4 key details, action button
- Grid: CSS Grid with auto-fit: `grid-template-columns: repeat(auto-fit, minmax(280px, 1fr))`

**Empty States:**
- Always design for zero-data scenarios
- Show illustration or icon
- Helpful message: "No [items] yet"
- Primary CTA: "+ Create your first [item]"

### Search & Filtering

**Search Bar:**
- Prominent placement: Header or top of content area
- Min-width: 250px on desktop
- Placeholder text: "Search [items]..."
- Search icon inside input (left side)
- Clear/X button when text entered
- Live search (debounced) or search button

**Filters:**
- **Placement**: Left sidebar or collapsible panel above content
- **Mobile**: Drawer/modal triggered by "Filter" button
- **Types**: 
  - Checkboxes for categories/tags
  - Date range pickers
  - Dropdowns for status/type
  - Sliders for numeric ranges
- **Show active filters** as removable chips/tags above results
- "Clear All Filters" option

### Loading & Feedback Patterns

**Loading States:**
1. **Initial page load**: Skeleton screens or spinner
2. **Data fetching**: Spinner or progress bar in content area
3. **Button actions**: Disable button + spinner: "Saving..."
4. **Inline updates**: Subtle spinner near updated element

**Success/Error Messages:**
1. **Toast/Snackbar**: Top-right corner, auto-dismiss 3-5 seconds
   - Success: Green with checkmark icon
   - Error: Red with X icon
   - Info: Blue with info icon
   
2. **Alert Boxes**: Top of content area, manually dismissible
   - Use for important multi-action errors
   
3. **Inline Messages**: Below form/section for contextual feedback

**Progress Indication:**
- Multi-step forms: Horizontal step indicator (1→2→3)
- File uploads: Progress bar with percentage
- Long processes: Estimated time or "Processing..." message

### Responsive Breakpoints & Behavior

**Standard Breakpoints:**
```css
/* Mobile First */
/* Small: 576px and up */
/* Medium: 768px and up */
/* Large: 992px and up */
/* X-Large: 1200px and up */
```

**Responsive Patterns:**
1. **Tables → Cards**: Convert table rows to stacked cards on mobile
2. **Multi-column → Single**: Stack columns vertically
3. **Sidebar → Drawer**: Off-canvas navigation
4. **Horizontal tabs → Accordion**: For 4+ tabs
5. **Fixed positioning → Static**: Avoid fixed elements on small screens
6. **Touch targets**: Minimum 44x44px for mobile buttons/links

### Accessibility Requirements

**Required ARIA Labels:**
- Landmark roles: `role="banner"`, `role="main"`, `role="navigation"`, `role="complementary"`, `role="contentinfo"`
- Form labels: Every input must have associated `<label>` or `aria-label`
- Buttons: Descriptive text or `aria-label` for icon-only buttons
- Dynamic content: `aria-live="polite"` for updates

**Keyboard Navigation:**
- Logical tab order (top-left → bottom-right)
- Skip navigation link (first focusable element)
- Modal focus trap (Tab cycles within modal)
- Escape key closes modals/dropdowns
- Enter key submits forms, activates buttons
- Arrow keys for menus/dropdowns

**Color & Contrast:**
- Minimum contrast ratio 4.5:1 for text
- Don't rely on color alone (use icons + text)
- Error states: Icon + color + text

**Focus Indicators:**
- Visible focus outline on all interactive elements
- Never `outline: none` without custom alternative
- Enhanced focus styles: `outline: 2px solid blue; outline-offset: 2px;`

### Action Patterns & Confirmations

**Bulk Actions:**
1. Checkboxes in first table column
2. "Select all" checkbox in header
3. Action bar appears at top when items selected
4. Show count: "3 items selected"
5. Actions: Delete, Export, Archive, etc.

**Contextual Menus:**
- Three-dot (⋮) or gear icon for per-item actions
- Dropdown menu with Edit, Delete, Duplicate, etc.
- Position: Right side of row or card
- Close on outside click or Escape key

**Confirmation Dialogs:**
- Use for destructive actions (Delete, Discard Changes)
- Modal overlay with backdrop
- Clear heading: "Delete [Item Name]?"
- Explanation of consequences
- Two buttons: Cancel (default) and Confirm (destructive color)

### Performance & UX Optimization

**Pagination vs. Infinite Scroll:**
- **Pagination**: Default for most data tables (predictable, accessible)
- **Infinite scroll**: For feeds, galleries (include "Load More" button as fallback)
- Show total count: "Page 1 of 24" or "Showing 1-25 of 573"

**Data Loading:**
- Load critical content first (above-the-fold)
- Lazy load images and below-fold content
- Cache frequently accessed data
- Show stale data while refreshing (optimistic UI)

**Auto-save:**
- For long forms or content editors
- Debounce saves (1-2 seconds after typing stops)
- Show "Saved" indicator with timestamp
- Draft recovery on session restore

### Component Examples by App Type

**Dashboard:**
- Top: Key metrics in cards (3-4 across)
- Middle: Chart/graph of primary data
- Bottom: Recent activity table or list
- Sidebar: Quick actions, filters, or navigation

**List/Index Page:**
- Header: Title + "+ New" button + Search
- Filters: Left sidebar or top panel
- Content: Table or card grid
- Bottom: Pagination controls

**Detail/Show Page:**
- Header: Title, metadata, "Edit" and "Delete" buttons
- Content: Sections in cards/panels (Details, Description, Related Items)
- Sidebar: Quick actions, tags, metadata
- Bottom: Related items or activity log

**Form/Edit Page:**
- Header: "Create [Item]" or "Edit [Item]"
- Content: Form fields in logical sections
- Bottom: "Save" and "Cancel" buttons
- Sidebar: Help text, tips, or preview

**Settings Page:**
- Left sidebar: Settings categories (Profile, Security, Notifications)
- Content: Active setting section with forms
- Each section: Save independently or single "Save All" at bottom

---

## Code Implementation Preferences

When generating code using this stack:

1. **HTML Structure:**
   - Use Bootstrap grid system: `.container`, `.row`, `.col-*`
   - Semantic HTML5: `<header>`, `<nav>`, `<main>`, `<article>`, `<aside>`, `<footer>`
   - OOCSS naming convention for custom classes: `.container`

2. **Forms with Bootstrap:**
   ```html
   <form>
     <div class="mb-3">
       <label for="input-id" class="form-label">Label *</label>
       <input type="text" class="form-control" id="input-id" required>
       <div class="invalid-feedback">Error message</div>
     </div>
   </form>
   ```

3. **JavaScript/jQuery:**
   - Use jQuery for DOM manipulation and AJAX with this stack
   - Prefer vanilla JS for modern features (fetch API acceptable)
   - Debounce search/autosave functions

4. **PHP/MySQL:**
   - Use PDO with prepared statements (prevent SQL injection)
   - Separate concerns: Controllers handle routing, Models handle data
   - Validate input server-side (never trust client)
   - Return JSON for AJAX endpoints

5. **Responsive CSS:**
   ```css
   /* Mobile first */
   .element { /* mobile styles */ }
   
   @media (min-width: 768px) {
     .element { /* tablet styles */ }
   }
   
   @media (min-width: 1200px) {
     .element { /* desktop styles */ }
   }
   ```

---

**When suggesting UI solutions, always:**
1. Start with mobile layout, then scale up
2. Include accessibility attributes
3. Consider empty, loading, and error states
4. Provide clear visual hierarchy
5. Use Bootstrap components where applicable
6. Ensure keyboard navigation works
7. Include form validation (client and server)
8. Add appropriate ARIA labels
9. Consider performance implications
10. Follow the principle of least surprise (use familiar patterns)
