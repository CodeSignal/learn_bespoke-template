# BESPOKE GENERALIZED COMPONENTS - IMPLEMENTATION CONTEXT

This document provides precise implementation instructions for creating embedded applications using the Bespoke generalized components. Follow these instructions exactly to ensure consistency across all applications.

## REQUIRED FILES STRUCTURE

Every application MUST include these files in the following order:

1. Design System CSS files (from design-system submodule)
2. help-modal.js (help system)
3. app.js (application logic)
4. server.js (server)

## HTML TEMPLATE IMPLEMENTATION

1. REPLACE the following placeholders in index.html EXACTLY as specified:

   a) `<!-- APP_TITLE -->`
      Replace with your application's page title
      Example: "Database Designer" or "Task Manager"

   b) `<!-- APP_NAME -->`
      Replace with your application's display name (appears in header)
      Example: "Database Designer" or "Task Manager"

   c) `<!-- APP_SPECIFIC_MAIN_CONTENT -->`
      Add your application's main content area
      Example: `<div id="canvas"></div>` or `<div id="editor"></div>`

   d) `<!-- APP_SPECIFIC_CSS -->`
      Add links to your application-specific CSS files
      Example: `<link rel="stylesheet" href="./my-app.css" />`

   e) `<!-- APP_SPECIFIC_SCRIPTS -->`
      Add links to your application-specific JavaScript files
      Example: `<script src="./my-app-logic.js"></script>`

3. DO NOT modify the core structure (header, script loading order, etc.)

## CSS IMPLEMENTATION

1. INCLUDE the design-system CSS files in your HTML (already included in index.html template):
   - Foundations: colors, spacing, typography
   - Components: button, boxes, input, dropdown, icons, tags

2. USE design-system CSS custom properties for styling:
   - Colors: `--Colors-*` variables (see design-system/colors/README.md)
   - Spacing: `--UI-Spacing-*` variables (see design-system/spacing/README.md)
   - Typography: `--Fonts-*` variables (see design-system/typography/README.md)

3. USE design-system component classes:
   - Buttons: `.button`, `.button-primary`, `.button-secondary`, `.button-tertiary`, `.button-danger`
   - Boxes: `.box`, `.box.card` for card-style containers
   - Inputs: `.input` class for text/number inputs

4. FOR custom styling, create app-specific CSS files
5. OVERRIDE design-system variables in your app-specific CSS if needed
6. FOLLOW design-system naming conventions for consistency

## JAVASCRIPT IMPLEMENTATION

1. HELP MODAL SETUP:
   a) Create help content using help-content-template.html as reference
   b) Initialize HelpModal with:
      - triggerSelector: `'#btn-help'`
      - content: your help content (string or loaded from file)
      - theme: `'auto'`

2. STATUS MANAGEMENT:
   a) Use the provided setStatus() function for status updates
   b) Update status for: loading, saving, errors, user actions
   c) Keep status messages concise and informative

## ERROR HANDLING REQUIREMENTS

1. WRAP all async operations in try-catch blocks
2. PROVIDE meaningful error messages to users
3. LOG errors to console for debugging
4. IMPLEMENT retry logic for network operations
5. HANDLE localStorage quota exceeded errors
6. VALIDATE data before saving operations

## STATUS MESSAGE CONVENTIONS

Use these EXACT status messages for consistency:

- "Ready" - Application loaded successfully
- "Loading..." - Data is being loaded
- "Saving..." - Data is being saved
- "Changes saved" - Auto-save completed successfully
- "Save failed (will retry)" - Server save failed, will retry
- "Failed to load data" - Data loading failed
- "Auto-save initialized" - Auto-save system started

## FILE NAMING CONVENTIONS

1. CSS files: kebab-case (e.g., my-app.css, task-manager.css)
2. JavaScript files: kebab-case (e.g., my-app.js, task-manager.js)
3. Data files: kebab-case (e.g., solution.json, initial-data.json)
4. Image files: kebab-case (e.g., overview.png, help-icon.svg)

---

# DESIGN SYSTEM USAGE GUIDELINES

This section explains how to use the design-system for embedded applications.

## OVERVIEW
The design-system provides reusable components and design tokens that can be embedded in any website. The design-system uses CSS custom properties and component classes for consistent styling.

## BASIC USAGE

### 1. Include the Design System CSS
The HTML template already includes all necessary design-system CSS files:
- Foundations: colors, spacing, typography
- Components: button, boxes, input, dropdown, icons, tags

### 2. Use the Component Classes
```html
<header>
  <h1>My App</h1>
  <div id="status">Ready</div>
  <button class="button button-secondary">Help</button>
</header>

<main>
  <aside>
    <section class="box card">
      <h2>Settings</h2>
      <form>
        <label>Name
          <input type="text" class="input" placeholder="Enter name" />
        </label>
        <button type="submit" class="button button-primary">Save</button>
      </form>
    </section>
  </aside>

  <div>
    <!-- Main content -->
  </div>
</main>
```

## COMPONENT REFERENCE

### LAYOUT COMPONENTS

#### Header
```html
<header>
  <h1>App Title</h1>
  <div id="status">Status message</div>
  <button class="button button-secondary">Help</button>
</header>
```

Note: Layout classes like `.header`, `.sidebar`, `.main-layout`, `.content-area` are not provided by the design-system. You may need to create custom layout styles or use semantic HTML with your own CSS.

#### Cards
```html
<section class="box card">
  <h2>Card Title</h2>
  <h3>Subtitle</h3>
  <p>Card content goes here</p>
</section>
```

### FORM COMPONENTS

#### Labels
```html
<!-- Vertical label -->
<label>Field Name
  <input type="text" class="input" placeholder="Enter text" />
</label>
```

Note: The design-system does not provide specific label or form layout classes. Use semantic HTML and create custom styles if needed.

#### Input Fields
```html
<!-- Text input (use .input class) -->
<input type="text" class="input" placeholder="Enter text" />

<!-- Number input -->
<input type="number" class="input" placeholder="Enter number" />
```

Note: The design-system provides `.input` class for text and number inputs. For other form elements (select, textarea, checkbox, radio, toggle), you may need to create custom styles or use native HTML elements.

#### Buttons
```html
<!-- Default button -->
<button class="button">Click Me</button>

<!-- Button variants -->
<button class="button button-primary">Primary Action</button>
<button class="button button-danger">Delete</button>
<button class="button button-secondary">Secondary</button>
<button class="button button-tertiary">Tertiary</button>

<!-- Button as link -->
<a href="#" class="button button-primary">Link Button</a>
```

### MODAL COMPONENTS

Note: The design-system does not provide modal components. The help-modal.js system creates modals dynamically. For custom modals, you may need to create your own modal styles or use a separate modal library.

## CUSTOMIZATION

### CSS Custom Properties
You can override design-system CSS custom properties to customize the appearance:

```css
:root {
  /* Override colors */
  --Colors-Base-Primary-700: #ff6b6b;
  --Colors-Base-Neutral-00: #f0f0f0;

  /* Override spacing */
  --UI-Spacing-spacing-m: 1.5rem;

  /* Override border radius */
  --UI-Radius-radius-m: 12px;
}
```

### Available Custom Properties

See the design-system documentation for complete variable lists:
- **Colors**: See `design-system/colors/README.md` for all color variables
- **Spacing**: See `design-system/spacing/README.md` for spacing and radius variables
- **Typography**: See `design-system/typography/README.md` for typography variables
- **Components**: Each component has its own variables (see component READMEs)

## THEME SUPPORT

### Automatic Dark Mode
The design-system automatically detects the user's system preference and switches between light and dark themes using `@media (prefers-color-scheme: dark)`. No additional configuration is needed.

## INTEGRATION EXAMPLES

### Database Designer
```html
<header>
  <h1>DB Schema Designer</h1>
  <button id="btn-save" class="button button-primary">Save</button>
  <div id="status">Ready</div>
  <button id="btn-help" class="button button-secondary">Help</button>
</header>

<main>
  <aside>
    <section class="box card">
      <h2>New Table</h2>
      <form>
        <label>Table name
          <input type="text" class="input" placeholder="users" />
        </label>
        <button type="submit" class="button button-primary">Add Table</button>
      </form>
    </section>
  </aside>

  <div>
    <!-- Diagram area -->
  </div>
</main>
```

## BEST PRACTICES

1. **Use design-system components**: Use provided component classes (`.button`, `.box`, `.input`, etc.)
2. **Use semantic HTML**: Combine with proper HTML elements for accessibility
3. **Customize via CSS variables**: Override design-system variables in your app-specific CSS
4. **Test in both themes**: Ensure your app works in light and dark modes
5. **Refer to design-system docs**: Check `design-system/README.md` and component READMEs for available classes and variables
