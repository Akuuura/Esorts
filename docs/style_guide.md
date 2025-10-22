# Shopify Theme Style Guide
## Based on Keith Williams' Everyday AI Website Design System

### Table of Contents
1. [Design Philosophy](#design-philosophy)
2. [Color System](#color-system)
3. [Typography](#typography)
4. [Spacing & Layout](#spacing--layout)
5. [Component Library](#component-library)
6. [Responsive Design](#responsive-design)
7. [Shopify Implementation](#shopify-implementation)

---

## Design Philosophy

**Explorer/Sage Aesthetic: Earthy, Natural, Grounded**
- **Trust-building**: Professional yet approachable
- **Modern simplicity**: Clean, uncluttered layouts
- **Natural warmth**: Earthy colors over stark whites/blacks
- **Accessibility-first**: High contrast ratios, readable fonts
- **Content-focused**: Typography and spacing that enhances readability

---

## Color System

### Primary Colors
```scss
// Core brand colors
--primary: #1d4035;          /* Darker forest teal - primary brand */
--primary-dark: #143028;     /* Darker variant for hover states */
--primary-light: #2c5f4f;    /* Lighter variant for backgrounds */

--secondary: #2d2d2d;        /* Warm charcoal - main text color */
--accent: #b85a1f;           /* Burnt sienna - call-to-action color */
```

### Success & Status Colors
```scss
--success: #6b9b37;          /* Natural green for success states */
--warning: #e5a845;          /* Warm yellow for warnings */
```

### Neutral Palette
```scss
--warm-white: #fefdfb;       /* Main background - slightly warm white */
--cream: #f7f5f0;            /* Section backgrounds */
--sand: #e8e4dc;             /* Borders and subtle backgrounds */
--stone: #d1cbc1;            /* Light text on dark backgrounds */
--gray-600: #4a4a4a;         /* Secondary text */
--gray-700: #333333;         /* Primary text (fallback) */
--gray-800: #2d2d2d;         /* Headers and emphasis */
--gray-900: #1a1a1a;         /* Maximum contrast text */
```

### Shopify Color Usage
- **Product prices**: `var(--accent)` for sale prices, `var(--gray-600)` for regular
- **Add to cart buttons**: `var(--accent)` background
- **Success messages**: `var(--success)`
- **Error states**: Use `#d32f2f` (not defined in original but needed for Shopify)
- **Out of stock**: `var(--gray-600)`

---

## Typography

### Font Stack
```scss
--font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
--font-mono: "SF Mono", Monaco, "Cascadia Code", "Roboto Mono", Consolas, monospace;
```

### Typography Scale
```scss
/* Heading Sizes */
.hero-title-main { font-size: 4rem; font-weight: 900; }      /* 64px */
.section-title { font-size: 2.75rem; font-weight: 900; }     /* 44px */
.subsection-title { font-size: 2rem; font-weight: 800; }     /* 32px */
.card-title { font-size: 1.75rem; font-weight: 700; }        /* 28px */
.component-title { font-size: 1.5rem; font-weight: 700; }    /* 24px */
.small-title { font-size: 1.25rem; font-weight: 700; }       /* 20px */

/* Body Text */
.hero-lead { font-size: 1.25rem; font-weight: 600; }         /* 20px */
.large-body { font-size: 1.125rem; font-weight: 400; }       /* 18px */
.body-text { font-size: 1rem; font-weight: 400; }            /* 16px */
.small-text { font-size: 0.875rem; font-weight: 500; }       /* 14px */
.caption { font-size: 0.75rem; font-weight: 600; }           /* 12px */
```

### Typography Implementation for Shopify
- **Product titles**: Use `.card-title` class
- **Product descriptions**: Use `.large-body` for excerpts, `.body-text` for full descriptions
- **Prices**: Use `.component-title` for main price, `.small-text` for compare-at price
- **Collection titles**: Use `.section-title`
- **Navigation**: Use `.small-text` with `font-weight: 600`

---

## Spacing & Layout

### Container System
```scss
--container-width: 1200px;
--section-padding: 5rem 2rem;  /* Vertical: 80px, Horizontal: 32px */

.container {
    max-width: var(--container-width);
    margin: 0 auto;
    padding: 0 2rem;
}
```

### Spacing Scale
```scss
/* Use these for consistent margins and padding */
.spacing-xs { margin/padding: 0.5rem; }    /* 8px */
.spacing-sm { margin/padding: 1rem; }      /* 16px */
.spacing-md { margin/padding: 1.5rem; }    /* 24px */
.spacing-lg { margin/padding: 2rem; }      /* 32px */
.spacing-xl { margin/padding: 3rem; }      /* 48px */
.spacing-2xl { margin/padding: 4rem; }     /* 64px */
.spacing-3xl { margin/padding: 6rem; }     /* 96px */
```

### Grid Systems
```scss
/* Product Grid - Responsive */
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

/* Two Column Layout */
.two-column {
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 4rem;
    align-items: center;
}

/* Cards Grid */
.cards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
}
```

---

## Component Library

### Buttons
```scss
/* Primary Button - Use for Add to Cart, Primary CTAs */
.btn-primary {
    background: var(--accent);
    color: var(--warm-white);
    padding: 1rem 2rem;
    border-radius: 8px;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    border: 2px solid var(--accent);
}

.btn-primary:hover {
    background: var(--primary);
    border-color: var(--primary);
    transform: translateY(-2px);
    box-shadow: 0 10px 25px rgb(29 64 53 / 20%);
}

/* Secondary Button - Use for View Product, Secondary Actions */
.btn-secondary {
    background: transparent;
    color: var(--secondary);
    border: 2px solid var(--stone);
    padding: 1rem 2rem;
    border-radius: 8px;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.btn-secondary:hover {
    background: var(--cream);
    border-color: var(--primary);
    color: var(--primary);
}
```

### Cards
```scss
/* Product Card */
.product-card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 10%);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    overflow: hidden;
}

.product-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 25px -5px rgb(0 0 0 / 10%);
}

/* Feature Card */
.feature-card {
    background: var(--cream);
    padding: 2.5rem;
    border-radius: 12px;
    border: 2px solid var(--sand);
    transition: all 0.3s ease;
}

.feature-card:hover {
    border-color: var(--primary);
    box-shadow: 0 10px 15px -3px rgb(0 0 0 / 10%);
}

/* Testimonial Card */
.testimonial-card {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 10%);
    border-left: 4px solid var(--primary);
}
```

### Navigation
```scss
/* Navigation Bar */
.nav {
    position: sticky;
    top: 0;
    background: rgba(254, 253, 251, 0.95);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid var(--sand);
    z-index: 1000;
    padding: 1rem 0;
}

/* Logo Styling */
.logo-main {
    font-size: 1.75rem;
    font-weight: 900;
    color: var(--primary);
    letter-spacing: -0.02em;
    line-height: 1;
}

.logo-sub {
    font-size: 0.625rem;
    font-weight: 600;
    color: var(--primary);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    opacity: 0.85;
}
```

### Forms
```scss
/* Form Input */
.form-input {
    width: 100%;
    padding: 1rem 1.5rem;
    border: 2px solid var(--sand);
    border-radius: 8px;
    font-size: 1rem;
    background: var(--warm-white);
    color: var(--secondary);
    transition: border-color 0.3s ease;
}

.form-input:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(29, 64, 53, 0.1);
}

/* Form Label */
.form-label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 600;
    color: var(--secondary);
    font-size: 0.875rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
}
```

---

## Responsive Design

### Breakpoints
```scss
/* Mobile First Approach */
/* Base styles: Mobile (up to 768px) */

@media (width >= 768px) {
    /* Tablet styles */
}

@media (width >= 1024px) {
    /* Desktop styles */
}

@media (width >= 1200px) {
    /* Large desktop styles */
}
```

### Responsive Patterns
```scss
/* Hero Section - Stacks on mobile */
.hero-grid {
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 4rem;
    align-items: center;
}

@media (width <= 768px) {
    .hero-grid {
        grid-template-columns: 1fr;
        gap: 3rem;
        text-align: center;
    }
}

/* Product Grid - Responsive columns */
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

@media (width <= 768px) {
    .product-grid {
        grid-template-columns: 1fr;
        gap: 1.5rem;
    }
}
```

---

## Shopify Implementation

### Theme Settings Schema
```json
{
  "name": "Colors",
  "settings": [
    {
      "type": "color",
      "id": "color_primary",
      "label": "Primary Color",
      "default": "#1d4035"
    },
    {
      "type": "color", 
      "id": "color_accent",
      "label": "Accent Color",
      "default": "#b85a1f"
    },
    {
      "type": "color",
      "id": "color_background",
      "label": "Background Color", 
      "default": "#fefdfb"
    }
  ]
}
```

### CSS Custom Properties in Liquid
```liquid
<!-- In layout/theme.liquid -->
<style>
  :root {
    --primary: {{ settings.color_primary }};
    --accent: {{ settings.color_accent }};
    --warm-white: {{ settings.color_background }};
    --secondary: #2d2d2d;
    --cream: #f7f5f0;
    --sand: #e8e4dc;
    --stone: #d1cbc1;
  }
</style>
```

### Product Card Implementation
```liquid
<!-- snippets/product-card.liquid -->
<div class="product-card">
  <div class="product-image">
    <img src="{{ product.featured_image | img_url: '400x400' }}" 
         alt="{{ product.title }}" 
         loading="lazy">
  </div>
  <div class="product-info">
    <h3 class="card-title">{{ product.title }}</h3>
    <div class="product-price">
      {% if product.compare_at_price > product.price %}
        <span class="price-sale">{{ product.price | money }}</span>
        <span class="price-compare">{{ product.compare_at_price | money }}</span>
      {% else %}
        <span class="price-regular">{{ product.price | money }}</span>
      {% endif %}
    </div>
    <a href="{{ product.url }}" class="btn-primary">
      <span>Add to Cart</span>
      <span class="btn-arrow">→</span>
    </a>
  </div>
</div>
```

### Collection Page Layout
```liquid
<!-- templates/collection.liquid -->
<div class="collection-header">
  <h1 class="section-title">{{ collection.title }}</h1>
  {% if collection.description != blank %}
    <p class="large-body">{{ collection.description }}</p>
  {% endif %}
</div>

<div class="product-grid">
  {% for product in collection.products %}
    {% render 'product-card', product: product %}
  {% endfor %}
</div>
```

### Section Example
```liquid
<!-- sections/featured-collection.liquid -->
<section class="featured-collection" style="padding: var(--section-padding);">
  <div class="container">
    {% if section.settings.title != blank %}
      <div class="section-header">
        <h2 class="section-title">{{ section.settings.title }}</h2>
        {% if section.settings.description != blank %}
          <p class="section-intro">{{ section.settings.description }}</p>
        {% endif %}
      </div>
    {% endif %}

    <div class="cards-grid">
      {% for product in collections[section.settings.collection].products limit: section.settings.products_to_show %}
        {% render 'product-card', product: product %}
      {% endfor %}
    </div>

    {% if section.settings.show_view_all %}
      <div style="text-align: center; margin-top: 3rem;">
        <a href="{{ collections[section.settings.collection].url }}" class="btn-secondary">
          View All Products
        </a>
      </div>
    {% endif %}
  </div>
</section>

{% schema %}
{
  "name": "Featured Collection",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Heading",
      "default": "Featured Collection"
    },
    {
      "type": "textarea",
      "id": "description", 
      "label": "Description"
    },
    {
      "type": "collection",
      "id": "collection",
      "label": "Collection"
    },
    {
      "type": "range",
      "id": "products_to_show",
      "min": 2,
      "max": 12,
      "step": 2,
      "label": "Products to show",
      "default": 6
    },
    {
      "type": "checkbox",
      "id": "show_view_all",
      "label": "Show 'View all' button"
    }
  ],
  "presets": [
    {
      "name": "Featured Collection",
      "category": "Collection"
    }
  ]
}
{% endschema %}
```

### CSS Organization for Shopify
```scss
/* assets/application.scss */

/* 1. CSS Reset & Variables */
@import 'base/reset';
@import 'base/variables';

/* 2. Base Styles */
@import 'base/typography';
@import 'base/layout';

/* 3. Components */
@import 'components/buttons';
@import 'components/cards';
@import 'components/forms';
@import 'components/navigation';

/* 4. Sections */
@import 'sections/header';
@import 'sections/hero';
@import 'sections/collection';
@import 'sections/product';
@import 'sections/footer';

/* 5. Templates */
@import 'templates/product';
@import 'templates/collection'; 
@import 'templates/cart';
@import 'templates/checkout';
```

---

## Key Implementation Notes

1. **Maintain Accessibility**: All color combinations maintain WCAG AA contrast ratios
2. **Performance**: Use CSS custom properties for theme customization
3. **Mobile-First**: All layouts are mobile-first responsive
4. **Loading States**: Implement skeleton screens using the sand/cream colors
5. **Error States**: Use warm colors for errors instead of harsh reds
6. **Focus States**: Always include focus styles for keyboard navigation

This design system creates a cohesive, trustworthy, and professional e-commerce experience that maintains the warm, approachable aesthetic of your original website while meeting all Shopify theme requirements.