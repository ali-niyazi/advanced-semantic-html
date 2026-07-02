# Module 14: HTML Templates, Slots, & Shadow DOM (Web Components)

## 🧠 Core Philosophy

**Web Components** enable developers to build reusable, encapsulated, and framework-agnostic UI components using native browser APIs.

The standard is built on **three core technologies**:

| Technology          | Purpose                                                                         |
| ------------------- | ------------------------------------------------------------------------------- |
| `<template>`        | Stores inert HTML fragments until JavaScript clones them.                       |
| **Shadow DOM**      | Creates an isolated DOM tree with encapsulated styles.                          |
| **Custom Elements** | Allows developers to define their own HTML elements by extending `HTMLElement`. |

---

# 📄 The `<template>` Element

The `<template>` element stores HTML that **is not rendered immediately**.

Its contents remain **inert** until cloned with JavaScript.

Characteristics:

- Not rendered.
- Images are not downloaded.
- Scripts do not execute.
- Exists as a `DocumentFragment`.

The template contents are accessible through:

```javascript
template.content;
```

---

## Cloning a Template

```javascript
const template = document.getElementById("star-rating-template").content;

const clone = template.cloneNode(true);

document.body.appendChild(clone);
```

### Rendering Flow

1. Locate the template.
2. Access its `content`.
3. Clone the fragment.
4. Append it into the live DOM (or a Shadow Root).

---

# 📥 The `<slot>` Element

Slots act as **placeholders** inside a template.

Content provided by the page (the **Light DOM**) is projected into these placeholders.

---

## Default Slot

If no matching slotted content exists, the slot displays its fallback content.

```html
<slot> Default Content </slot>
```

---

## Named Slot

Assign a name to the slot.

```html
<slot name="star-rating-legend">
  <legend>Rate your experience:</legend>
</slot>
```

---

## Consuming the Slot

```html
<star-rating>
  <legend slot="star-rating-legend">User Rating</legend>
</star-rating>
```

The browser automatically inserts the `<legend>` into the matching named slot.

---

# 🏷️ Custom Elements

Custom elements allow developers to create entirely new HTML tags.

Example:

```html
<star-rating></star-rating>
```

---

## Browser Resilience

Browsers **do not fail** when encountering unknown HTML elements.

Before registration, an element such as:

```html
<star-rating></star-rating>
```

behaves similarly to an anonymous inline element (`<span>`):

- No default styling
- No built-in behavior
- No semantic meaning

---

## Registering a Custom Element

```javascript
customElements.define(
  "star-rating",

  class extends HTMLElement {
    constructor() {
      super();

      const templateContent = document.getElementById(
        "star-rating-template",
      ).content;

      const shadowRoot = this.attachShadow({
        mode: "open",
      });

      shadowRoot.appendChild(templateContent.cloneNode(true));
    }
  },
);
```

### Important

Always call:

```javascript
super();
```

as the first statement inside the constructor.

---

# 👤 Shadow DOM

Shadow DOM creates a completely isolated DOM tree.

```javascript
this.attachShadow({
  mode: "open",
});
```

Benefits include:

- Style encapsulation
- DOM encapsulation
- Predictable component behavior
- Reduced CSS conflicts

---

## Style Isolation

Styles inside the Shadow DOM:

✅ Cannot leak into the page.

Styles outside the Shadow DOM:

✅ Cannot accidentally style internal component elements.

---

# 🎯 CSS Selectors Inside Shadow DOM

Because styles are scoped, selector specificity becomes much simpler.

Instead of writing:

```css
.page .card form button
```

you can often write:

```css
button
```

without affecting the surrounding page.

---

## `:host`

Targets the custom element itself.

```css
:host {
  display: block;
}
```

---

## `:host(selector)`

Targets the host only when it matches a selector.

```css
:host(.active) {
  border: 2px solid green;
}
```

---

## `::slotted()`

Styles content projected into a slot.

```css
::slotted(legend) {
  font-weight: bold;
}
```

Only the slotted element itself can be styled—not its descendants.

---

# 🌉 Styling Across the Shadow Boundary

Sometimes component authors want consumers to customize specific internal elements.

Use the **CSS Shadow Parts** specification.

---

## Exposing a Part

```html
<template id="star-rating-template">
  <form part="form-container">...</form>
</template>
```

---

## Styling from Global CSS

```css
star-rating::part(form-container) {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
}
```

This allows controlled customization while preserving encapsulation.

---

# ✅ Key Takeaways

- Web Components are built on **Templates**, **Shadow DOM**, and **Custom Elements**.
- `<template>` stores inert HTML until cloned.
- `<slot>` enables Light DOM content projection.
- Browsers gracefully handle unknown custom elements before registration.
- Custom elements extend `HTMLElement`.
- Always call `super()` inside constructors.
- Shadow DOM isolates both DOM structure and CSS.
- Use `:host` to style the component itself.
- Use `::slotted()` to style projected content.
- Use `::part()` to expose internal elements for safe external theming.
