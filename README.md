# Order Summary Component

## Overview

The **Order Summary Component** is a responsive UI card built with **HTML5** and **CSS3** only — no JavaScript, no CSS frameworks. It displays a clean summary of a subscription plan (Annual Plan, $59.99/year) with a call-to-action button and a cancel link. The project was built as a front-end challenge to practice modern CSS layout techniques, responsive design, and accessible semantic HTML.

This project is ideal for beginner to intermediate developers who want to see how a polished, production-ready UI component can be built from scratch with just HTML and CSS.

---

## Features

- **Responsive design** — adapts seamlessly across desktop, tablet, and mobile.
- **Semantic HTML** — uses `<main>`, `<header>`, `<section>`, `<h1>`, `<button>`, and more for meaningful structure.
- **CSS Flexbox layout** — powers the centering of the card and the plan row.
- **CSS custom properties (variables)** — centralizes colors, spacing, typography, border radius, and shadows for easy theming.
- **Hover effects** — smooth transitions on buttons, links, and interactive elements.
- **Accessible structure** — focus-visible outlines, meaningful alt text, keyboard-navigable links and buttons.
- **Pure CSS styling** — zero JavaScript, zero external CSS libraries.
- **Clean and maintainable code** — organized into logical sections with CSS custom properties.

---

## Technologies Used

| Technology      | Purpose                               |
| --------------- | ------------------------------------- |
| HTML5           | Semantic page structure               |
| CSS3            | All styling and layout                |
| Google Fonts    | Red Hat Display typeface              |
| CSS Variables   | Centralized design tokens             |
| Flexbox         | Layout and alignment                  |
| Media Queries   | Responsive breakpoints                |
| SVG             | Scalable vector icons and illustrations |

---

## Project Structure

```
order-summary-component/
│
├── index.html           # Main HTML document
├── CSS 
    ├── styles.css           # All styles (no inline or embedded CSS)
├── images/
│   ├── favicon-32x32.png           # Browser tab icon
│   ├── illustration-hero.svg       # Hero illustration at top of card
│   ├── icon-music.svg              # Music note icon in the plan box
│   ├── pattern-background-desktop.svg  # Background wave (desktop)
│   └── pattern-background-mobile.svg   # Background wave (mobile)
└── README.md            # Project documentation (this file)
```

### File Purposes

- **`index.html`** — Contains the complete page markup. Every visible element on the page is defined here using semantic HTML tags.
- **`styles.css`** — Contains all visual styling. The stylesheet is organized into sections: Reset, Variables, Layout, Components, and Responsive.
- **`images/`** — Houses all visual assets. SVGs are used for the hero illustration, icon, and background patterns, keeping file sizes small and resolution-independent.
- **`README.md`** — This documentation file.

---

## HTML Structure

The HTML is organized into a single `<main>` element that wraps the entire card. Within it, content is divided into logical sections:

```html
<main class="card">
  <header class="card__hero">
    <img src="./images/illustration-hero.svg" alt="..." class="card__hero-img" />
  </header>

  <section class="card__content">
    <h1 class="card__title">Order Summary</h1>

    <p class="card__description">
      You can now listen to millions of songs, audiobooks, and podcasts on
      any device anywhere you like!
    </p>

    <div class="plan">
      <div class="plan__icon">
        <img src="./images/icon-music.svg" alt="" class="plan__icon-img" />
      </div>
      <div class="plan__details">
        <span class="plan__name">Annual Plan</span>
        <span class="plan__price">$59.99/year</span>
      </div>
      <a href="#" class="plan__change">Change</a>
    </div>

    <button class="btn btn--primary" type="button">Proceed to Payment</button>

    <a href="#" class="card__cancel">Cancel Order</a>
  </section>
</main>
```

### Section Breakdown

| Element                 | Tag              | Purpose                                                        |
| ----------------------- | ---------------- | -------------------------------------------------------------- |
| **Card container**      | `<main>`         | Wraps the entire component. Using `<main>` tells browsers and assistive technology that this is the primary content of the page. |
| **Hero section**        | `<header>`       | Contains the illustration. Using `<header>` here is semantically appropriate as it is introductory content for the card. |
| **Hero image**          | `<img>`          | Displays the illustration at full card width. The `alt` text describes the image for screen readers. |
| **Content section**     | `<section>`      | Groups the textual content, plan box, and actions into a logical region. |
| **Title**               | `<h1>`           | The primary heading of the card. Only one `<h1>` per page is best practice. |
| **Description**         | `<p>`            | A paragraph of body text explaining the subscription benefits.   |
| **Plan box**            | `<div>`          | A container for the plan details. A `<div>` is appropriate here because it is a presentational grouping, not a semantic landmark. |
| **Plan name**           | `<span>`         | Inline element for the plan title ("Annual Plan").              |
| **Plan price**          | `<span>`         | Inline element for the price text.                              |
| **Change link**         | `<a>`            | A hyperlink for changing the plan. Keyboard-accessible by default. |
| **Payment button**      | `<button>`       | A native `<button>` element, which is keyboard-focusable and can be activated with Enter or Space. |
| **Cancel link**         | `<a>`            | A hyperlink styled as a text link for cancelling the order.      |

---

## CSS Architecture

The stylesheet is divided into six major sections, each clearly labelled:

```
/* ----- RESET ----- */
/* ----- VARIABLES ----- */
/* ----- BODY / LAYOUT ----- */
/* ----- CARD ----- */
/* ----- BUTTONS ----- */
/* ----- RESPONSIVE ----- */
```

### 1. Reset

```css
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

Removes default browser margins and padding, and sets `box-sizing: border-box` so that padding and borders are included in an element's total width — making sizing much more predictable.

### 2. CSS Variables (Custom Properties)

All design tokens are stored in `:root` variables, making the theme easy to update in one place:

```css
:root {
  --clr-bg: #E9EDFF;
  --clr-primary: #382AE1;
  --ff-primary: 'Red Hat Display', sans-serif;
  --space-16: 1rem;
  --radius-lg: 1.375rem;
  --shadow-card: 0 20px 40px -12px rgba(56, 42, 225, 0.2);
  /* ... more variables ... */
}
```

These variables are reused throughout the stylesheet. To change the entire color scheme, you only need to update the variable values here.

### 3. Global Styles

The `<body>` uses Flexbox to center the card both horizontally and vertically, and applies the background color and wave pattern:

```css
body {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--clr-bg);
  background-image: url('./images/pattern-background-desktop.svg');
  background-repeat: no-repeat;
  background-size: 100% auto;
}
```

### 4. Layout

The card uses `overflow: hidden` so its children respect the parent's `border-radius`. The content section inside the card is a Flexbox column that centers everything:

```css
.card__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-20);
  padding: var(--space-40) var(--space-48) var(--space-48);
}
```

### 5. Components

Each major piece of UI — the plan box, buttons, links — has its own class styles. The plan box uses Flexbox to arrange the icon, text details, and "Change" link in a row:

```css
.plan {
  display: flex;
  align-items: center;
  gap: var(--space-20);
  background-color: var(--clr-plan-bg);
  border-radius: var(--radius-sm);
  padding: var(--space-20) var(--space-24);
}
```

### 6. Buttons

The `.btn` class provides shared button styles, while `.btn--primary` extends it with specific colors and shadow effects. Hover and active states use CSS transitions:

```css
.btn--primary:hover {
  background-color: var(--clr-primary-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-btn-hover);
}

.btn--primary:active {
  transform: translateY(0);
}
```

### 7. Responsive Styles

Media queries at 768px and 480px adjust padding, font sizes, and layout for smaller screens.

---

## Color Palette

| Color            | Hex       | CSS Variable       | Purpose                             |
| ---------------- | --------- | ------------------ | ----------------------------------- |
| Lavender         | `#E9EDFF` | `--clr-bg`         | Page background                     |
| White            | `#FFFFFF` | `--clr-card`       | Card background                     |
| Dark Navy        | `#1F2F56` | `--clr-heading`    | Main heading text                   |
| Gray-Blue        | `#7280A7` | `--clr-body`       | Body text, cancel link              |
| Light Gray       | `#F8F9FE` | `--clr-plan-bg`    | Plan box background                 |
| Royal Blue       | `#382AE1` | `--clr-primary`    | Primary button, accent links        |
| Lighter Blue     | `#766CF1` | `--clr-primary-hover` | Button hover state              |

---

## Typography

| Property            | Value                                   |
| ------------------- | --------------------------------------- |
| Font family         | `Red Hat Display` (Google Fonts)        |
| Font weights used   | `500` (regular), `700` (bold), `900` (black) |
| Base font size      | `1rem` (16px)                           |

### Text Hierarchy

```css
/* Heading — largest, boldest */
.card__title {
  font-size: 1.625rem;   /* 26px */
  font-weight: 900;       /* Black */
}

/* Body description */
.card__description {
  font-size: 1rem;        /* 16px */
  font-weight: 500;
  line-height: 1.625;
}

/* Plan details / button / cancel link */
.plan__name, .plan__price, .btn, .card__cancel {
  font-size: 0.9375rem;   /* 15px */
}

/* Change link — smallest */
.plan__change {
  font-size: 0.8125rem;   /* 13px */
}
```

---

## Layout

### Centering

The card is centered on the page using Flexbox on the `<body>`:

```css
body {
  display: flex;
  align-items: center;     /* Vertical center */
  justify-content: center; /* Horizontal center */
  min-height: 100vh;       /* Full viewport height */
}
```

### Spacing System

Spacing follows an **8px grid**, converted to `rem` units for accessibility:

| Token        | Rem  | Pixels |
| ------------ | ---- | ------ |
| `--space-8`  | 0.5rem  | 8px  |
| `--space-12` | 0.75rem | 12px |
| `--space-16` | 1rem    | 16px |
| `--space-20` | 1.25rem | 20px |
| `--space-24` | 1.5rem  | 24px |
| `--space-32` | 2rem    | 32px |
| `--space-40` | 2.5rem  | 40px |
| `--space-48` | 3rem    | 48px |

Using `rem` units ensures spacing scales with the user's browser font-size settings, improving accessibility.

### Border Radius

| Token           | Rem       | Pixels | Usage                     |
| --------------- | --------- | ------ | ------------------------- |
| `--radius-sm`   | 0.75rem   | 12px   | Plan box, buttons         |
| `--radius-lg`   | 1.375rem  | 22px   | Card container            |

### Shadows

```css
--shadow-card: 0 20px 40px -12px rgba(56, 42, 225, 0.2),
               0 8px 24px -6px rgba(56, 42, 225, 0.1);
--shadow-btn: 0 12px 24px -6px rgba(56, 42, 225, 0.3);
--shadow-btn-hover: 0 16px 32px -8px rgba(56, 42, 225, 0.4);
```

Layered shadows create a modern, elevated Card UI. The button shadow increases on hover to reinforce the "lifting" effect.

---

## Responsive Design

### Desktop (> 768px)

- Card is centered with a fixed `max-width: 420px`.
- Full wave background pattern displayed.
- Generous padding and font sizes.

### Tablet (481px – 768px)

```css
@media (max-width: 768px) {
  .card__content {
    padding: var(--space-32) var(--space-24) var(--space-32);
  }
  .card__title {
    font-size: 1.375rem;
  }
}
```

- Switches to the mobile-optimised background pattern.
- Reduces padding and slightly scales down font sizes.

### Mobile (≤ 480px)

```css
@media (max-width: 480px) {
  .card {
    max-width: 90%;
  }
  .card__content {
    padding: var(--space-24);
  }
  .plan {
    flex-wrap: wrap;
    justify-content: center;
  }
}
```

- Card width becomes 90% of the viewport.
- Padding reduced further.
- Plan box wraps its content to stack vertically on very narrow screens.

---

## Accessibility

The project includes several accessibility best practices:

| Practice                    | Implementation                                               |
| --------------------------- | ------------------------------------------------------------ |
| **Semantic HTML**           | Uses `<main>`, `<header>`, `<section>`, `<h1>`, `<button>`, `<a>` for meaningful structure. |
| **Alt text**                | The hero image has descriptive `alt` text. The music icon has `alt=""` (decorative, hidden from screen readers). |
| **Keyboard navigation**     | All interactive elements (`<a>`, `<button>`) are natively keyboard-focusable. |
| **Focus indicators**        | A `:focus-visible` outline is added to all interactive elements, appearing only when navigating via keyboard. |
| **Color contrast**          | Text colors are chosen to meet WCAG contrast guidelines (e.g., `#1F2F56` on white for headings, `#7280A7` on `#F8F9FE` for plan text). |
| **`rem` units**             | Using `rem` for font sizes and spacing respects user browser font-size preferences. |

---

## Customization Guide

Developers can quickly customise the component by editing the CSS variables in `:root`:

### Change Colors

```css
:root {
  --clr-primary: #your-color;
  --clr-primary-hover: #your-hover-color;
  --clr-bg: #your-background-color;
}
```

### Change Font

```css
:root {
  --ff-primary: 'Inter', sans-serif;
}
```

Then import the font in `index.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@500;700;900&display=swap" rel="stylesheet">
```

### Change Card Width

```css
.card {
  max-width: 500px; /* default was 420px */
}
```

### Change Border Radius

```css
:root {
  --radius-lg: 1rem;    /* 16px — reduces card rounding */
  --radius-sm: 0.5rem;  /* 8px  — reduces button rounding */
}
```

### Change Shadows

```css
:root {
  --shadow-card: 0 10px 30px rgba(0, 0, 0, 0.1);
}
```

### Change Spacing

Adjust the spacing variables — for example, to use a 4px grid instead of 8px:

```css
:root {
  --space-8: 0.25rem;   /* was 0.5rem  */
  --space-16: 0.5rem;   /* was 1rem    */
  --space-24: 1rem;     /* was 1.5rem  */
}
```

---

## Browser Compatibility

This project uses standard CSS features that work in all modern browsers:

| Browser           | Supported |
| ----------------- | --------- |
| Chrome            | ✅ Yes    |
| Firefox           | ✅ Yes    |
| Safari            | ✅ Yes    |
| Edge              | ✅ Yes    |
| Opera             | ✅ Yes    |
| Samsung Internet  | ✅ Yes    |

No vendor prefixes are needed for the CSS features used (Flexbox, CSS variables, media queries, transitions) in current browser versions.

---

## Performance Considerations

- **Zero JavaScript** — no JS parsing, execution, or blocking.
- **No external CSS libraries** — no Bootstrap, Tailwind, or other framework overhead.
- **SVG images** — vector graphics scale beautifully and have small file sizes compared to raster images (PNG, JPG).
- **One Google Font** — only a single font family is loaded, minimising network requests.
- **Minimal HTTP requests** — 1 HTML file, 1 CSS file, a few SVG images.
- **Fast rendering** — the layout uses simple Flexbox, which browsers can compute very quickly.

---

## Possible Improvements

While the project is complete as-is, here are ideas for extending it:

- **Dark mode** — Add a `prefers-color-scheme: dark` media query that swaps to a dark palette.
- **Theme switcher** — Use a checkbox + CSS custom properties (or a tiny bit of JS) to toggle themes.
- **CSS animations** — Add a subtle entrance animation (e.g., fade-in + slide-up) for the card on page load.
- **Form integration** — Replace the static plan box with a radio-button group that lets users choose between Annual and Monthly plans.
- **Backend payment processing** — Connect the "Proceed to Payment" button to a checkout API (requires JavaScript and a backend).
- **Accessibility enhancements** — Add `aria-live` regions for dynamic content, or skip-to-content links for keyboard users.

---

## Lessons Learned

This project demonstrates several core front-end concepts:

1. **Semantic HTML** — Choosing the right tag for the right purpose improves accessibility, SEO, and code readability.
2. **CSS Flexbox** — A single-direction layout tool that handles centering, alignment, and spacing with minimal code.
3. **CSS Custom Properties** — Centralising design tokens makes theming and maintenance straightforward.
4. **Responsive Design** — Media queries + relative units (`rem`, `%`, `ch`) create layouts that adapt to any screen size.
5. **The 8px Grid** — A systematic approach to spacing creates visual harmony and consistency.
6. **Button and Link States** — Designing `:hover`, `:active`, and `:focus-visible` states improves usability and polish.
7. **BEM-like Naming** — A naming convention (`.card__title`, `.plan__name`) keeps CSS predictable and avoids specificity conflicts.

---

## Conclusion

The **Order Summary Component** is a compact but complete front-end project that showcases how to build a polished, responsive, and accessible UI card using nothing but HTML and CSS. It is an excellent learning resource for developers who want to strengthen their understanding of modern CSS layout techniques, responsive design principles, and clean code organisation. By studying and extending this project, developers can gain confidence in writing production-quality CSS from scratch.
