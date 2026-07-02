# Module 18: Disclosure Widgets (`<details>` & `<summary>`)

## 🧠 Core Philosophy

Disclosure widgets allow users to **expand or collapse content on demand** without leaving the current page.

Before HTML5, developers typically built accordions and expandable panels using JavaScript or CSS hacks (such as hidden checkboxes).

Today, HTML provides a native solution:

- `<details>`
- `<summary>`

These elements provide:

- Native keyboard accessibility
- Built-in screen reader support
- Automatic state management
- No JavaScript required for basic functionality

They are ideal for:

- FAQs
- Accordions
- Expandable sections
- Disclosure panels
- Progressive disclosure of content

---

# 🛠️ Anatomy of a Disclosure Widget

## `<details>`

The parent container that wraps expandable content.

```html
<details>...</details>
```

---

## `<summary>`

Defines the visible heading that users interact with.

```html
<details>
  <summary>Shipping Information</summary>

  <p>Orders arrive within 3–5 business days.</p>
</details>
```

### Important

`<summary>` should be the **first child** of `<details>`.

Although browsers may recover from incorrect markup, following this structure ensures consistent behavior and accessibility.

---

## The `open` Attribute

`open` is a Boolean attribute controlling the widget's initial state.

```html
<details open>
  <summary>FAQ</summary>

  <p>Visible by default.</p>
</details>
```

When present:

- Content is expanded.

When absent:

- Only the summary is visible.

---

# ⚡ Native Behavior

Browsers automatically handle interaction.

Users can toggle a disclosure widget by:

- Mouse click
- Touch
- <kbd>Enter</kbd>
- <kbd>Space</kbd>

No JavaScript is required.

When toggled, the browser automatically adds or removes the `open` attribute.

---

# 📄 DOM Behavior

Collapsing a `<details>` element **does not remove its contents from the DOM**.

Instead:

- Content remains in the document.
- Scripts can still access it.
- State is simply hidden from rendering.

---

# 🎨 Styling the Disclosure Marker

Browsers display a built-in disclosure marker (typically a triangle).

The marker can be styled using `::marker`.

```css
details summary::marker {
  color: royalblue;
  font-size: 1.2rem;
}
```

Support varies slightly between browsers, but modern browsers generally support styling the marker.

---

# ✨ Creating a Custom Indicator

Many designs replace the default triangle with custom icons.

## Remove the Native Marker

```css
details summary {
  list-style: none;
}

details summary::-webkit-details-marker {
  display: none;
}
```

The second selector improves compatibility with older versions of Safari and Chromium.

---

## Add a Custom Symbol

```css
details summary::before {
  content: "+";
  font-weight: bold;
  margin-right: 0.5rem;
}

details[open] summary::before {
  content: "−";
}
```

This creates a classic accordion using plus/minus symbols.

---

# ♿ Accessibility Considerations

One of the biggest advantages of `<details>` is its built-in accessibility.

Benefits include:

- Keyboard support
- Screen reader announcements
- Automatic expanded/collapsed state management

For most use cases, **native disclosure widgets are preferable to custom JavaScript accordions.**

---

## Keyboard Navigation

`<summary>` is naturally keyboard-focusable.

Users can toggle it using:

- <kbd>Enter</kbd>
- <kbd>Space</kbd>

> **Note:** Older versions of Safari had inconsistent keyboard support for `<summary>`, but current versions have significantly improved.

---

## Avoid Nested Interactive Elements

Do **not** place interactive controls inside `<summary>`.

For example:

```html
<!-- Avoid -->

<summary>
  Read More

  <a href="#">Help</a>
</summary>
```

Nested interactive elements can:

- Break keyboard navigation
- Cause conflicting click behavior
- Produce inconsistent screen reader output

Keep `<summary>` simple.

---

# 🔍 Search Behavior

In Chromium-based browsers (Chrome, Edge):

- Hidden content inside `<details>` is searchable.
- When a search match is found, the browser automatically expands the disclosure widget.

Firefox and Safari currently behave differently, so this feature should not be relied upon for critical functionality.

---

# ⚠️ Omitting `<summary>`

If a `<details>` element has no `<summary>`:

```html
<details>
  <p>Hidden content</p>
</details>
```

Browsers generate a default summary (typically labeled **"Details"**) internally.

Because this generated summary lives inside the browser's shadow DOM:

- It is difficult to style.
- The wording is browser-defined.

**Always provide your own `<summary>` element.**

---

# 🔌 The `HTMLDetailsElement` API

The DOM provides a dedicated interface for `<details>`.

---

## The `open` Property

Read or modify the current state.

```javascript
const details = document.querySelector("details");

details.open = true;
```

or

```javascript
details.open = false;
```

Equivalent to adding or removing the `open` attribute.

---

## The `toggle` Event

Whenever the disclosure widget opens or closes, it dispatches a `toggle` event.

```javascript
const details = document.querySelector("details");

details.addEventListener("toggle", () => {
  console.log(details.open);
});
```

Useful for:

- Analytics
- Lazy loading
- Synchronizing UI state

---

# 🪗 Building an Exclusive Accordion

Native `<details>` elements do **not** automatically close other open sections.

To create a traditional accordion, listen for the `toggle` event.

```javascript
const accordions = document.querySelectorAll("details");

accordions.forEach((current) => {
  current.addEventListener("toggle", () => {
    if (!current.open) return;

    accordions.forEach((other) => {
      if (other !== current) {
        other.open = false;
      }
    });
  });
});
```

Only one section remains open at a time.

---

# ✅ Best Practices

- Use `<details>` instead of JavaScript for simple disclosure widgets.
- Always include a `<summary>` as the first child.
- Let the browser manage the `open` attribute whenever possible.
- Keep `<summary>` concise and free of nested interactive elements.
- Prefer native accessibility over custom accordion implementations.
- Customize disclosure markers with CSS only when necessary.
- Use the `toggle` event to enhance—not replace—native behavior.

---

# ✅ Key Takeaways

- `<details>` creates an expandable disclosure container.
- `<summary>` provides the interactive heading.
- The `open` attribute controls the expanded state.
- Native disclosure widgets include built-in keyboard and accessibility support.
- Hidden content remains in the DOM when collapsed.
- `::marker` and `::before` can customize disclosure indicators.
- Chromium browsers can automatically reveal search matches inside collapsed `<details>`.
- The `HTMLDetailsElement` API exposes the `open` property and `toggle` event.
- JavaScript can build exclusive accordions while preserving native accessibility.
