# Advanced CSS3 & Responsive Architecture

A standalone, framework-free CSS3 stylesheet demonstrating modern responsive architecture: design tokens, fluid typography, container queries, logical properties, and layout primitives that scale without relying on dozens of media queries.

## Files

- `advanced-responsive.css` — self-contained stylesheet, no build step or dependencies

## Architecture overview

| Section | Purpose |
|---|---|
| Design Tokens | Custom properties for color, spacing, type, radius, shadow, motion |
| Reset / Base | Minimal reset, reduced-motion support, sensible image defaults |
| Layout Primitives | Reusable structural classes (`.container`, `.grid-auto`, `.cluster`, `.with-sidebar`, `.stack`) |
| Components | `.card`, `.btn` — built entirely from tokens, no hard-coded values |
| Container Queries | Components that adapt to their parent's size, not the viewport |
| Breakpoints | Mobile-first media queries, used only where fluid CSS isn't enough |
| Utilities | Small single-purpose helper classes |

## Key techniques

- **Fluid values with `clamp()`** — spacing and font sizes scale smoothly across viewport widths instead of jumping at fixed breakpoints
- **Container queries** (`container-type: inline-size`) — a component like `.card` reflows based on the width of its own parent, so it looks right whether it's in a sidebar or a full-width section
- **Logical properties** (`padding-inline`, `margin-block-start`) — layout adapts automatically for right-to-left languages, unlike `left`/`right`/`top`
- **Auto-fit grid** (`.grid-auto`) — adds or removes columns as space allows, no breakpoint math required
- **Flexbox "sidebar" pattern** (`.with-sidebar`) — sidebar and content wrap to a single column automatically once they can't both fit
- **Dark mode** — via `prefers-color-scheme`, plus a manual `[data-theme="dark"]` class for a JS-driven toggle
- **Accessibility-aware motion** — `prefers-reduced-motion` disables transitions/animations for users who request it
- **Print stylesheet** — hides non-print elements and forces readable colors

## How to use

Link the stylesheet in your HTML `<head>`:

```html
<link rel="stylesheet" href="advanced-responsive.css">
```

Then apply the provided classes to your markup, for example:

```html
<div class="container">
  <div class="with-sidebar">
    <aside class="sidebar">…</aside>
    <div class="content stack">
      <div class="card-container">
        <div class="card">
          <h3 class="card-title">Title</h3>
          <p class="card-body">Body text</p>
        </div>
      </div>
    </div>
  </div>
</div>
```

## Browser support notes

- **Container queries** and `color-mix()` require a modern browser (Chrome/Edge 105+, Firefox 110+, Safari 16+). For older browsers, the layout still works but components fall back to their default (non-container-aware) styling.
- All other techniques (`clamp()`, logical properties, `auto-fit` grid) have broad modern support.

## Customization

- All colors, spacing, and type scale live in the `:root` custom properties at the top of the file — change values there rather than overriding individual rules
- Add new components by composing existing tokens (`var(--space-md)`, `var(--color-accent)`, etc.) rather than hard-coding new values
- Toggle dark mode manually by setting `document.documentElement.dataset.theme = "dark"` in JS

## Related

- Companion HTML file: `semantic-accessibility-demo.html` (semantic structure & accessibility demo from the earlier project)
