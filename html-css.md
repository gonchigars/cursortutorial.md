# CSS Fundamentals: Building an E-commerce Page

This tutorial guides you through core CSS concepts, explaining each with text diagrams. We'll build toward a complete e-commerce page, using Cursor AI to generate code based on our understanding.

## Understanding Key CSS Concepts

### 1. The Box Model: Foundation of CSS Layout

Every HTML element is a box with four layers that determine its size and spacing:

```
+-----------------------------------------------+
|                    MARGIN                     | ← Space outside the element
|    +-----------------------------------+      |
|    |             BORDER                |      | ← Element outline
|    |    +-------------------------+    |      |
|    |    |        PADDING          |    |      | ← Inner spacing
|    |    |    +--------------+     |    |      |
|    |    |    |   CONTENT    |     |    |      | ← The actual content
|    |    |    +--------------+     |    |      |
|    |    |                         |    |      |
|    |    +-------------------------+    |      |
|    |                                   |      |
|    +-----------------------------------+      |
|                                               |
+-----------------------------------------------+
```

**How it works:**
- **Content**: The text, image, or other media
- **Padding**: Space between content and border
- **Border**: Line around the padding
- **Margin**: Space outside the border, between elements

**The critical box-sizing property:**

```
content-box (default):     border-box (recommended):
width: 200px               width: 200px
+------------------+       +------------------+
|    content       |       |    content       |
|    200px wide    |       |    adjusts to    |
+------------------+       |    fit container |
|  + padding 20px  |       |                  |
|  + border 2px    |       |                  |
|  = 244px total   |       |  200px total     |
+------------------+       +------------------+
```

**Impact on design:**
- With `content-box`, adding padding or borders increases the element's total width
- With `border-box`, the element maintains its defined width, and content area shrinks to accommodate padding and borders

**Practical application:**
```css
/* Makes all elements use border-box for more predictable layouts */
*, *::before, *::after {
  box-sizing: border-box;
}
```

### 2. CSS Grid: Page-Level Layout System

CSS Grid provides a two-dimensional layout system ideal for overall page structure:

```
GRID LAYOUT:
+---------------------------------------------------+
|                    HEADER                         | ← Grid Area 1
+------------+--------------------------------+-----+
|            |                                |     |
|  SIDEBAR   |          MAIN CONTENT          |     | ← Grid Areas 2-3
|  (Filters) |          (Products)            |     |
|            |                                |     |
+------------+--------------------------------+-----+
|                    FOOTER                         | ← Grid Area 4
+---------------------------------------------------+

CSS: 
.container {
  display: grid;
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "footer footer footer";
  grid-template-columns: 250px 1fr 1fr;
}
```

**Key Grid properties:**
- `grid-template-columns`: Defines column widths
- `grid-template-rows`: Defines row heights
- `grid-template-areas`: Creates named template areas
- `grid-gap`: Adds space between grid items

**Practical application:**
```css
/* Page layout with named grid areas */
.container {
  display: grid;
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "footer footer footer";
  grid-template-columns: 250px 1fr 1fr;
  gap: 20px;
}

/* Placing elements in grid areas */
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main-content { grid-area: main; }
.footer { grid-area: footer; }
```

### 3. Flexbox: Component-Level Layout

Flexbox excels at one-dimensional layouts, perfect for components like navigation bars, card layouts, and more:

```
FLEXBOX:

Row layout (default):       Column layout:
+---+---+---+---+           +-------+
| 1 | 2 | 3 | 4 |           |   1   |
+---+---+---+---+           +-------+
                            |   2   |
                            +-------+
                            |   3   |
                            +-------+
                            |   4   |
                            +-------+

FLEXBOX ALIGNMENT:
justify-content (main axis):
+---+---+---+              +---+---+---+
|1|2|3|        |           |   |1|2|3|   |
+---+---+---+              +---+---+---+
flex-start                 center

align-items (cross axis):
+-------+                  +-------+
|1|     |                  |       |
+-------+                  |1|     |
|2|     |                  +-------+
+-------+                  |2|     |
flex-start                 center
```

**How the Box Model affects Flexbox:**

Flexbox containers and items still follow the box model:

```
FLEX CONTAINER WITH BOX MODEL:
+------------------------------------------------+
|                  CONTAINER MARGIN              |
|  +------------------------------------------+  |
|  |              CONTAINER BORDER            |  |
|  |  +--------------------------------------+ |  |
|  |  |          CONTAINER PADDING           | |  |
|  |  |  +-----+   +-----+   +-----+        | |  |
|  |  |  |ITEM1|   |ITEM2|   |ITEM3|        | |  |
|  |  |  |     |   |     |   |     |        | |  |
|  |  |  +-----+   +-----+   +-----+        | |  |
|  |  |                                      | |  |
|  |  +--------------------------------------+ |  |
|  +------------------------------------------+  |
+------------------------------------------------+

INDIVIDUAL FLEX ITEM WITH BOX MODEL:
+-----------------------------------+
|           ITEM MARGIN             |
|  +----------------------------+   |
|  |        ITEM BORDER         |   |
|  |  +----------------------+  |   |
|  |  |     ITEM PADDING     |  |   |
|  |  |  +--------------+    |  |   |
|  |  |  | ITEM CONTENT |    |  |   |
|  |  |  +--------------+    |  |   |
|  |  |                      |  |   |
|  |  +----------------------+  |   |
|  +----------------------------+   |
+-----------------------------------+
```

**Spacing in Flexbox:**
- **Margins** create space between flex items
- **Padding** creates space inside each flex item
- **gap** property adds consistent spacing between items (newer than margins)

**Practical application:**
```css
/* Navigation bar with Flexbox */
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem; /* Padding inside the nav container */
}

.nav-links {
  display: flex;
  gap: 2rem; /* Space between nav links */
}

.nav-link {
  padding: 0.5rem 1rem; /* Clickable area inside each link */
}
```

### 4. CSS Variables (Custom Properties)

CSS Variables allow you to define values once and reuse them throughout your stylesheet:

```
CSS VARIABLE DEFINITION AND USAGE:

:root {
  --primary-color: #3B82F6;
  --text-color: #1F2937;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
}

ELEMENT STYLING WITH VARIABLES:
+-----------------------------------+
|         Product Card              |
|  border: 1px solid var(--border-color);
|  padding: var(--spacing-md);     |
|                                  |
|  .card-title {                   |
|    color: var(--text-color);     |
|    margin-bottom: var(--spacing-sm);
|  }                               |
|                                  |
|  .card-button {                  |
|    background: var(--primary-color);
|    padding: var(--spacing-sm) var(--spacing-md);
|  }                               |
+-----------------------------------+
```

**Benefits:**
- Creates consistent design
- Makes site-wide changes easier
- Enables theming (light/dark modes)

**Practical application:**
```css
:root {
  /* Colors */
  --color-primary: #3B82F6;
  --color-secondary: #1E40AF;
  --color-accent: #EF4444;
  --color-text: #1F2937;
  --color-text-light: #6B7280;
  --color-background: #FFFFFF;
  --color-border: #E5E7EB;
  
  /* Spacing */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
  --spacing-xl: 4rem;
  
  /* Typography */
  --font-family: 'Inter', sans-serif;
  --font-size-sm: 0.875rem;
  --font-size-md: 1rem;
  --font-size-lg: 1.25rem;
  --font-size-xl: 1.5rem;
}
```

### 5. Responsive Design

Responsive design ensures your website works on all screen sizes:

```
RESPONSIVE LAYOUTS:

Desktop Layout:             Tablet Layout:              Mobile Layout:
(1024px+)                   (768px-1023px)               (under 768px)
+-----+-------------+       +-----+-------------+       +-------------+
|     |             |       |     |             |       |   Header    |
|  S  |    Main     |       |  S  |    Main     |       +-------------+
|  i  |   Content   |       |  i  |   Content   |       |  Sidebar    |
|  d  |             |       |  d  |             |       +-------------+
|  e  |             |       |  e  |             |       |    Main     |
|     |             |       |     |             |       |   Content   |
+-----+-------------+       +-----+-------------+       +-------------+

MEDIA QUERY STRUCTURE:
@media (max-width: 768px) {
  /* Mobile Styles */
  .container {
    grid-template-areas:
      "header"
      "sidebar"
      "main"
      "footer";
    grid-template-columns: 1fr;
  }
}
```

**Key responsive techniques:**
- Media queries to apply different styles at different screen sizes
- Relative units (%, rem, em) instead of fixed pixels
- Flexible layouts with Grid and Flexbox
- Mobile-first or desktop-first approach

**Practical application:**
```css
/* Base styles (mobile-first) */
.product-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

/* Tablet */
@media (min-width: 768px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .product-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

## Putting It All Together: E-Commerce Page Structure

Now that we understand the key concepts, let's sketch our e-commerce page structure:

```
E-COMMERCE PAGE LAYOUT:
+---------------------------------------------------+
|                    HEADER                         |
|  [Logo]    [Navigation]           [Cart] [Login]  |
+------------+--------------------------------+-----+
|            |                                |     |
|  FILTERS   |        PRODUCT GRID            |     |
|            |                                |     |
|  [Category]|  +-------+  +-------+  +-------+     |
|  [Price]   |  | Card  |  | Card  |  | Card  |     |
|  [Ratings] |  +-------+  +-------+  +-------+     |
|            |                                |     |
|            |  +-------+  +-------+  +-------+     |
|            |  | Card  |  | Card  |  | Card  |     |
|            |  +-------+  +-------+  +-------+     |
|            |                                |     |
+------------+--------------------------------+-----+
|                     FOOTER                        |
|  [Links]   [Contact]   [Social]   [Newsletter]    |
+---------------------------------------------------+
```

### Product Card Structure

```
PRODUCT CARD:
+----------------------------------+
|          [Image]                 |
|                                  |
|  Product Title                   |
|  $24.99        ★★★★☆             |
|                                  |
|  Short description text that     |
|  explains the product briefly    |
|                                  |
|  [Add to Cart]                   |
+----------------------------------+
```

## Building the E-Commerce Page with Cursor AI

Now that we understand the concepts, let's use AI to generate our e-commerce page. We'll break this into two steps:

### Step 1: Generate the HTML Structure

**Prompt for Cursor AI:**
```
Create the semantic HTML structure for an e-commerce product listing page with:

1. A header with:
   - Logo
   - Primary navigation (Home, Products, Categories, About, Contact)
   - Cart icon with item counter
   - Login/account button


  2.  sidebar for filters including:
     - Category checkboxes
     - Price range slider
     - Rating filter

3. Main page
   - A product grid showing 6 product cards, each with:
     - Product image
     - Product title
     - Price
     - Rating (stars)
     - Short description
     - "Add to Cart" button

4. A footer with:
   - Company links
   - Contact information
   - Social media icons
   - Newsletter signup form

Use semantic HTML elements and add appropriate class names following BEM methodology. Don't include any CSS yet, just the HTML structure.
```

### Step 2: Generate the CSS

After reviewing the HTML, use this prompt to generate the CSS:

**Prompt for Cursor AI:**
```
Create comprehensive CSS for the e-commerce product listing page that applies all the concepts we've discussed:

1. Start with a CSS reset and set box-sizing: border-box for all elements

2. Define CSS variables (custom properties) for:
   - A cohesive color scheme (primary, secondary, accent, and neutral colors)
   - Typography (font family, sizes, weights, line heights)
   - Spacing values (for consistent margins and padding)
   - Border-radius and shadow values

3. Create the layout structure using CSS Grid:
   - Create a grid container for the entire page
   - Define grid template areas for header, sidebar, main content, and footer
   - Make the product grid responsive with different numbers of columns at different breakpoints

4. Style components using Flexbox:
   - Header navigation and controls
   - Filter sidebar sections
   - Individual product cards
   - Footer sections

5. Add responsive design with media queries:
   - Mobile view: stacked layout with collapsible filters
   - Tablet view: sidebar and content side by side with 2 product columns
   - Desktop view: full layout with 3 product columns

6. Apply the box model appropriately:
   - Use margin for spacing between components
   - Use padding for internal spacing
   - Add borders and shadows to create visual separation

7. Add interaction styles:
   - Hover effects for buttons and product cards
   - Active/focus states for interactive elements

Include detailed comments explaining how each CSS concept is being applied throughout the stylesheet.
```

## Understanding and Customizing the Result

After receiving the generated code:

1. **Identify how each concept is applied:**
   - Where is CSS Grid used vs. Flexbox?
   - How are CSS variables organized?
   - How does the responsive design adapt at different breakpoints?
   - How does the box model create appropriate spacing?

2. **Experiment with changes:**
   - Modify CSS variables to create a different color scheme
   - Adjust grid template areas to change the layout
   - Change spacing values to see how they affect the design
   - Add new features like a "Sale" badge to product cards

3. **Common customizations to try:**
   - Change the number of product columns at different breakpoints
   - Modify the header to be sticky (fixed at the top while scrolling)
   - Add a dark mode theme using CSS variables
   - Enhance card hover effects with transforms or transitions

## Beyond the Basics: Next Steps

After mastering these fundamentals, you might explore:

1. **CSS Animations and Transitions** for more interactive elements
2. **CSS Preprocessors** like Sass or Less for more powerful styling
3. **CSS Frameworks** like Tailwind or Bootstrap for rapid development
4. **CSS-in-JS** approaches for component-based styling
5. **CSS Grid** for more complex layouts

## Conclusion

By understanding these core CSS concepts—the box model, CSS Grid, Flexbox, CSS variables, and responsive design—you now have the knowledge to create professional, responsive web layouts. The e-commerce page you built demonstrates how these concepts work together to create a complete, functional design.

Remember that CSS mastery comes with practice. Continue experimenting with different layouts and designs to reinforce your understanding of these fundamental concepts.
```
/* CSS Reset and Base Styles */
/* Reset margins, padding, and set box-sizing */
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* CSS Custom Properties (Variables) */
:root {
  /* Color Scheme */
  --color-primary: #2563eb;
  --color-primary-dark: #1d4ed8;
  --color-secondary: #64748b;
  --color-accent: #f59e0b;
  --color-success: #10b981;
  --color-danger: #ef4444;

  /* Neutral Colors */
  --color-white: #ffffff;
  --color-gray-100: #f1f5f9;
  --color-gray-200: #e2e8f0;
  --color-gray-300: #cbd5e1;
  --color-gray-400: #94a3b8;
  --color-gray-500: #64748b;
  --color-gray-600: #475569;
  --color-gray-700: #334155;
  --color-gray-800: #1e293b;
  --color-gray-900: #0f172a;
  --color-black: #000000;

  /* Typography */
  --font-family-primary: "Inter", system-ui, -apple-system, sans-serif;
  --font-size-xs: 0.75rem;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;
  --font-size-3xl: 1.875rem;
  --font-size-4xl: 2.25rem;

  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;

  --line-height-tight: 1.25;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;

  /* Spacing */
  --spacing-1: 0.25rem;
  --spacing-2: 0.5rem;
  --spacing-3: 0.75rem;
  --spacing-4: 1rem;
  --spacing-5: 1.25rem;
  --spacing-6: 1.5rem;
  --spacing-8: 2rem;
  --spacing-10: 2.5rem;
  --spacing-12: 3rem;
  --spacing-16: 4rem;

  /* Border Radius */
  --radius-sm: 0.25rem;
  --radius-md: 0.375rem;
  --radius-lg: 0.5rem;
  --radius-xl: 0.75rem;
  --radius-2xl: 1rem;

  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
}

/* Base Styles */
body {
  font-family: var(--font-family-primary);
  font-size: var(--font-size-base);
  line-height: var(--line-height-normal);
  color: var(--color-gray-800);
  background-color: var(--color-gray-100);
}

/* Layout Grid */
.main {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar products"
    "footer footer";
  grid-template-columns: 300px 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: var(--spacing-6);
  padding: var(--spacing-6);
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.products {
  grid-area: products;
}

.footer {
  grid-area: footer;
}

/* Header Styles */
.header__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: var(--color-white);
  padding: var(--spacing-4);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

.header__logo-image {
  height: 40px;
  width: auto;
}

.header__nav-list {
  display: flex;
  gap: var(--spacing-4);
  list-style: none;
}

.header__nav-link {
  text-decoration: none;
  color: var(--color-gray-700);
  font-weight: var(--font-weight-medium);
  padding: var(--spacing-2) var(--spacing-4);
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
}

.header__nav-link:hover {
  color: var(--color-primary);
  background-color: var(--color-gray-100);
}

.header__actions {
  display: flex;
  gap: var(--spacing-4);
  align-items: center;
}

.header__cart {
  display: flex;
  align-items: center;
  gap: var(--spacing-2);
  padding: var(--spacing-2) var(--spacing-4);
  background-color: var(--color-gray-100);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.2s ease;
}

.header__cart:hover {
  background-color: var(--color-gray-200);
}

.header__account {
  padding: var(--spacing-2) var(--spacing-4);
  background-color: var(--color-primary);
  color: var(--color-white);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.2s ease;
}

.header__account:hover {
  background-color: var(--color-primary-dark);
}

/* Sidebar Styles */
.sidebar__filters {
  background-color: var(--color-white);
  padding: var(--spacing-6);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

.sidebar__title {
  font-size: var(--font-size-xl);
  margin-bottom: var(--spacing-6);
  color: var(--color-gray-900);
}

.sidebar__filter-group {
  margin-bottom: var(--spacing-6);
}

.sidebar__filter-title {
  font-size: var(--font-size-lg);
  margin-bottom: var(--spacing-4);
  color: var(--color-gray-800);
}

.sidebar__category-list,
.sidebar__rating-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-3);
}

.sidebar__category-item,
.sidebar__rating-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-2);
  cursor: pointer;
}

.sidebar__price-slider {
  width: 100%;
  margin: var(--spacing-4) 0;
}

.sidebar__price-display {
  display: flex;
  justify-content: space-between;
  color: var(--color-gray-600);
}

/* Products Grid */
.products__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-6);
}

.product-card {
  background-color: var(--color-white);
  border-radius: var(--radius-lg);
  padding: var(--spacing-4);
  box-shadow: var(--shadow-md);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.product-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

.product-card__image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: var(--radius-md);
  margin-bottom: var(--spacing-4);
}

.product-card__title {
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  margin-bottom: var(--spacing-2);
}

.product-card__price {
  font-size: var(--font-size-xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  margin-bottom: var(--spacing-2);
}

.product-card__rating {
  color: var(--color-accent);
  margin-bottom: var(--spacing-2);
}

.product-card__description {
  color: var(--color-gray-600);
  margin-bottom: var(--spacing-4);
}

.product-card__add-to-cart {
  width: 100%;
  padding: var(--spacing-3) var(--spacing-4);
  background-color: var(--color-primary);
  color: var(--color-white);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.2s ease;
}

.product-card__add-to-cart:hover {
  background-color: var(--color-primary-dark);
}

/* Footer Styles */
.footer {
  background-color: var(--color-white);
  padding: var(--spacing-8);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

.footer__container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--spacing-8);
}

.footer__title {
  font-size: var(--font-size-lg);
  font-weight: var(--font-weight-semibold);
  margin-bottom: var(--spacing-4);
  color: var(--color-gray-900);
}

.footer__list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-2);
}

.footer__link {
  text-decoration: none;
  color: var(--color-gray-600);
  transition: color 0.2s ease;
}

.footer__link:hover {
  color: var(--color-primary);
}

.footer__contact {
  font-style: normal;
}

.footer__social {
  display: flex;
  gap: var(--spacing-4);
}

.footer__social-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background-color: var(--color-gray-100);
  border-radius: var(--radius-full);
  transition: all 0.2s ease;
}

.footer__social-link:hover {
  background-color: var(--color-gray-200);
  transform: translateY(-2px);
}

.footer__newsletter {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-3);
}

.footer__newsletter-input {
  padding: var(--spacing-3);
  border: 1px solid var(--color-gray-300);
  border-radius: var(--radius-md);
}

.footer__newsletter-button {
  padding: var(--spacing-3);
  background-color: var(--color-primary);
  color: var(--color-white);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 0.2s ease;
}

.footer__newsletter-button:hover {
  background-color: var(--color-primary-dark);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .products__grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .footer__container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .main {
    grid-template-areas:
      "header"
      "products"
      "footer";
    grid-template-columns: 1fr;
  }

  .sidebar {
    display: none; /* Will be shown as a collapsible menu in mobile */
  }

  .header__container {
    flex-direction: column;
    gap: var(--spacing-4);
  }

  .header__nav-list {
    flex-wrap: wrap;
    justify-content: center;
  }

  .products__grid {
    grid-template-columns: 1fr;
  }

  .footer__container {
    grid-template-columns: 1fr;
  }
}

/* Focus and Active States */
button:focus,
input:focus,
a:focus {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}

button:active,
a:active {
  transform: scale(0.98);
}

```css```
I'll explain the CSS code by relating it to the provided HTML structure, showing how each part affects the page layout and appearance using text diagrams.

## CSS Reset and Base Styles

```css
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**What/Why**: Resets all elements to have no margins or padding, and uses box-sizing: border-box so padding and borders don't increase element size.

**How/Where**:
```
Before Reset:       After Reset:
┌───────────┐      ┌─────────┐
│   Element │      │Element  │
│           │  →   │         │
│  (padded) │      │(no pad) │
└───────────┘      └─────────┘
```
Applied to every element in the HTML, ensuring consistent sizing behavior.

## CSS Variables (Custom Properties)

```css
:root {
  /* Color Scheme */
  --color-primary: #2563eb;
  /* ...more colors, typography, spacing, etc. */
}
```

**What/Why**: Defines reusable values for the entire document in a single place, making the design system consistent and easy to modify.

**How/Where**:
```
┌────────────────────────────────────────┐
│ :root {                                │
│   ┌─────────┐  ┌────────┐  ┌────────┐  │
│   │ Colors  │  │ Fonts  │  │Spacing │  │
│   └─────────┘  └────────┘  └────────┘  │
│ }                                      │
└───────────────┬────────────────────────┘
                │
                ▼
      Used throughout the document
      for consistent styling
```
These variables are referenced throughout the CSS using `var(--variable-name)`.

## Body Base Styles

```css
body {
  font-family: var(--font-family-primary);
  font-size: var(--font-size-base);
  line-height: var(--line-height-normal);
  color: var(--color-gray-800);
  background-color: var(--color-gray-100);
}
```

**What/Why**: Sets default styling for the entire document.

**How/Where**:
```
┌──────────────────────────────────────┐
│                                      │
│  <body> element (entire page)        │
│  - Font family: "Inter" or fallbacks │
│  - Font size: 1rem (16px)            │
│  - Line height: 1.5                  │
│  - Text color: Dark gray             │
│  - Background: Light gray            │
│                                      │
└──────────────────────────────────────┘
```
Applied to the `<body>` tag, affecting all content within the page.

## Layout Grid

```css
.main {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar products"
    "footer footer";
  grid-template-columns: 300px 1fr;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: var(--spacing-6);
  padding: var(--spacing-6);
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.products { grid-area: products; }
.footer { grid-area: footer; }
```

**What/Why**: Creates the overall page layout using CSS Grid with named areas.

**How/Where**:
```
Layout applied to <main class="main">:

┌───────────────────────────────────┐
│              HEADER               │ <- <header class="header">
├────────────────┬──────────────────┤
│                │                  │
│                │                  │
│                │                  │
│    SIDEBAR     │    PRODUCTS      │ <- <aside class="sidebar">
│    (300px)     │    (flexible)    │    <section class="products">
│                │                  │
│                │                  │
│                │                  │
├────────────────┴──────────────────┤
│              FOOTER               │ <- <footer class="footer">
└───────────────────────────────────┘

With 1.5rem (var(--spacing-6)) gaps between areas
```
Applied to the `<main>` element and its child sections.

## Header Styles

```css
.header__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: var(--color-white);
  padding: var(--spacing-4);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

/* Logo, navigation, and actions styling */
```

**What/Why**: Styles the header with a flex layout to position logo, navigation, and action buttons.

**How/Where**:
```
Applied to <div class="header__container">:

┌────────────────────────────────────────────────────┐
│                                                    │
│  ┌──────┐   ┌─────────────────────┐   ┌────────┐  │
│  │ LOGO │   │  NAV LINKS (flex)   │   │ACTIONS │  │
│  └──────┘   └─────────────────────┘   └────────┘  │
│                                                    │
└────────────────────────────────────────────────────┘

With white background, rounded corners, and subtle shadow
```
Applied to the container within the header with items distributed across space.

## Navigation Styling

```css
.header__nav-list {
  display: flex;
  gap: var(--spacing-4);
  list-style: none;
}

.header__nav-link {
  text-decoration: none;
  color: var(--color-gray-700);
  /* more styling */
}

.header__nav-link:hover {
  color: var(--color-primary);
  background-color: var(--color-gray-100);
}
```

**What/Why**: Creates a horizontal navigation menu with hover effects.

**How/Where**:
```
Applied to <ul class="header__nav-list">:

┌───────────────────────────────────────────────┐
│                                               │
│  Home  Products  Categories  About  Contact   │
│                                               │
└───────────────────────────────────────────────┘

Normal link:   [     Home     ]  (dark gray)
Hover state:   [     Home     ]  (blue text with light gray background)
```
Applied to the navigation list and its link items.

## Action Buttons

```css
.header__actions {
  display: flex;
  gap: var(--spacing-4);
  align-items: center;
}

.header__cart { /* styling */ }
.header__account { /* styling */ }
/* Hover states */
```

**What/Why**: Styles the cart and account buttons in the header.

**How/Where**:
```
Applied to <div class="header__actions">:

┌─────────────────────────────┐
│                             │
│  [🛒 0]    [Login/Account]  │
│  gray      blue background  │
│                             │
└─────────────────────────────┘

Cart hover:  Slightly darker gray
Account hover: Darker blue
```
Applied to the action buttons in the header's right section.

## Sidebar Filter Styles

```css
.sidebar__filters {
  background-color: var(--color-white);
  padding: var(--spacing-6);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

/* Filter groups and elements */
```

**What/Why**: Creates a styled container for filter options with different categories.

**How/Where**:
```
Applied to <section class="sidebar__filters">:

┌─────────────────────────────┐
│         FILTERS             │
│ ┌───────────────────────┐   │
│ │ Categories            │   │
│ │ □ Electronics         │   │
│ │ □ Clothing            │   │
│ │ □ Home & Kitchen      │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ Price Range           │   │
│ │ [===========|===]     │   │
│ │ $0           $1000    │   │
│ └───────────────────────┘   │
│ ┌───────────────────────┐   │
│ │ Rating                │   │
│ │ ○ ★★★★★              │   │
│ │ ○ ★★★★☆              │   │
│ │ ○ ★★★☆☆              │   │
│ └───────────────────────┘   │
└─────────────────────────────┘

White background with rounded corners and shadow
```
Applied to the sidebar filter section and its components.

## Products Grid

```css
.products__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-6);
}

.product-card { /* styling */ }
/* Product card elements */
```

**What/Why**: Creates a responsive grid of product cards, 3 columns on desktop.

**How/Where**:
```
Applied to <div class="products__grid">:

┌─────────┐ ┌─────────┐ ┌─────────┐
│ Product │ │ Product │ │ Product │
│    1    │ │    2    │ │    3    │
└─────────┘ └─────────┘ └─────────┘
┌─────────┐ ┌─────────┐ ┌─────────┐
│ Product │ │ Product │ │ Product │
│    4    │ │    5    │ │    6    │
└─────────┘ └─────────┘ └─────────┘

With 1.5rem spacing between cards
```
Applied to the product grid container holding all product cards.

## Product Card Styling

```css
.product-card {
  background-color: var(--color-white);
  border-radius: var(--radius-lg);
  padding: var(--spacing-4);
  box-shadow: var(--shadow-md);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.product-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

/* Product card elements */
```

**What/Why**: Styles each product card with consistent elements and hover effect.

**How/Where**:
```
Applied to <article class="product-card">:

┌───────────────────────┐     On hover:   ┌───────────────────────┐
│     [Product Image]   │                 │     [Product Image]   │
│                       │                 │                       │
│   Product Name        │       →        │   Product Name        │
│   $99.99              │                 │   $99.99              │
│   ★★★★☆              │     Rises       │   ★★★★☆              │
│   Short description   │     up by 4px   │   Short description   │
│                       │     with        │                       │
│   [   Add to Cart   ] │     larger      │   [   Add to Cart   ] │
└───────────────────────┘     shadow      └───────────────────────┘
```
Applied to each product card article and its children.

## Footer Styling

```css
.footer {
  background-color: var(--color-white);
  padding: var(--spacing-8);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}

.footer__container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--spacing-8);
}

/* Footer sections */
```

**What/Why**: Styles the footer with a 4-column grid layout for different sections.

**How/Where**:
```
Applied to <footer class="footer"> and inner <div class="footer__container">:

┌────────────────────────────────────────────────────────────────┐
│                                                                │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌───────────┐ │
│  │ Company    │  │ Contact    │  │ Follow Us  │  │Newsletter │ │
│  │ About Us   │  │ 123 Main   │  │            │  │           │ │
│  │ Careers    │  │ Street...  │  │ 📘 🐦 📸 💼 │  │ [Email  ] │ │
│  │ Press      │  │            │  │            │  │ [Submit  ] │ │
│  │ Blog       │  │            │  │            │  │           │ │
│  └────────────┘  └────────────┘  └────────────┘  └───────────┘ │
│                                                                │
└────────────────────────────────────────────────────────────────┘

White background with rounded corners and shadow
```
Applied to the footer and its container with four equal sections.

## Responsive Design

```css
@media (max-width: 1024px) {
  .products__grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .footer__container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .main {
    grid-template-areas:
      "header"
      "products"
      "footer";
    grid-template-columns: 1fr;
  }
  .sidebar { display: none; }
  /* More mobile adjustments */
}
```

**What/Why**: Adjusts layout for different screen sizes.

**How/Where**:
```
Desktop (>1024px):          Tablet (768-1024px):        Mobile (<768px):
┌─────────────────┐         ┌─────────────────┐         ┌─────────────┐
│     HEADER      │         │     HEADER      │         │   HEADER    │
├────────┬────────┤         ├────────┬────────┤         ├─────────────┤
│        │        │         │        │        │         │             │
│SIDEBAR │PRODUCTS│         │SIDEBAR │PRODUCTS│         │  PRODUCTS   │
│        │ 3 cols │         │        │ 2 cols │         │   1 col     │
│        │        │         │        │        │         │             │
├────────┴────────┤         ├────────┴────────┤         ├─────────────┤
│     FOOTER      │         │     FOOTER      │         │   FOOTER    │
│    (4 cols)     │         │    (2 cols)     │         │   (1 col)   │
└─────────────────┘         └─────────────────┘         └─────────────┘
```
Applied at specific breakpoints to adjust layouts for different devices.

## Focus and Active States

```css
button:focus,
input:focus,
a:focus {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}

button:active,
a:active {
  transform: scale(0.98);
}
```

**What/Why**: Improves accessibility and interaction feedback.

**How/Where**:
```
Normal button:   [     Button     ]
Focused state:   [     Button     ] + blue outline 2px away from edge
Active state:    [    Button    ] (slightly smaller when clicked)
```
Applied to all interactive elements (buttons, links, inputs) for accessibility and visual feedback.

This CSS systematically implements a complete, responsive e-commerce interface with consistent visual language, clear hierarchy, and appropriate interactive states that adapt to different devices and user interactions.
