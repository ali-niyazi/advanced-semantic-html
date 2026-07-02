# Module 16: Focus Management & Sequential Navigation Order

## 🧠 Core Philosophy

Keyboard focus is the foundation of **accessibility (A11y)**.

Users who rely on keyboards, screen readers, switch devices, or other assistive technologies navigate a page by moving **focus** between interactive elements.

For a predictable user experience:

> **The visual order of interactive elements should always match their logical DOM order.**

When focus moves unexpectedly or visually "jumps" around the page, keyboard navigation becomes confusing and can make an interface unusable.

---

# 🎯 Understanding Focus

Most native interactive HTML elements are **focusable** and participate in the natural Tab sequence automatically.

Examples include:

- `<a href>`
- `<button>`
- `<input>`
- `<select>`
- `<textarea>`
- `<summary>`

These elements should generally be preferred over custom implementations because they include built-in keyboard behavior and accessibility semantics.

---

# 🚫 Visual Order vs DOM Order

CSS can change the **visual layout** without changing the **keyboard navigation order**.

This creates a mismatch between what users see and where focus moves.

## Common Causes

### Flexbox

```css
.container {
  display: flex;
  flex-direction: row-reverse;
}
```

### Grid / Flex Order

```css
.item {
  order: 2;
}
```

Although the layout changes visually, pressing **Tab** still follows the original DOM order.

### Best Practice

Whenever possible:

- Write HTML in the correct logical order.
- Use CSS for styling—not to reorder meaningful content.

---

# ✅ Test the Focus Journey

Always verify keyboard navigation by testing:

- `Tab`
- `Shift + Tab`

Ensure that focus moves:

- Sequentially
- Predictably
- Logically
- Consistently across responsive layouts

---

# 👁️ Visible Focus Indicators

Never remove focus indicators without providing an accessible replacement.

Useful pseudo-classes include:

```css
:focus

:focus-visible

:focus-within
```

Example:

```css
button:focus-visible {
  outline: 3px solid royalblue;
  outline-offset: 3px;
}
```

### Why `:focus-visible`?

It primarily displays focus styles for keyboard users while avoiding unnecessary outlines during mouse interaction.

---

# 🛠️ The `tabindex` Attribute

`tabindex` controls whether an element participates in sequential keyboard navigation.

| Value         | Included in Tab Order | `element.focus()` | Typical Use                                                                           |
| ------------- | --------------------- | ----------------- | ------------------------------------------------------------------------------------- |
| `0`           | ✅ Yes                | ✅ Yes            | Make custom interactive elements keyboard-focusable.                                  |
| `-1`          | ❌ No                 | ✅ Yes            | Programmatically focus dialogs, drawers, notifications, or error summaries.           |
| `1` or higher | ✅ Yes                | ✅ Yes            | **Avoid.** Creates an artificial focus order that overrides the natural DOM sequence. |

---

## `tabindex="0"`

Adds an element to the natural tab order.

Example:

```html
<div role="button" tabindex="0">Share</div>
```

### Important

If an element mimics a native control, you must also implement the expected keyboard behavior.

For a button, that includes responding to:

- `Enter`
- `Space`

Whenever possible, prefer using a real:

```html
<button>Share</button>
```

instead of recreating one.

---

## `tabindex="-1"`

Removes an element from sequential keyboard navigation while allowing JavaScript to move focus to it.

Example:

```javascript
dialog.focus();
```

Common use cases:

- Modal dialogs
- Error summaries
- Off-screen navigation drawers
- Skip-link destinations

---

## 🚫 Positive `tabindex`

Avoid values greater than zero.

```html
<div tabindex="5"></div>
```

Problems include:

- Breaks natural reading order.
- Creates maintenance issues.
- Produces inconsistent keyboard navigation.

Modern accessibility guidelines strongly recommend relying on the DOM order instead.

---

# ⚡ `contenteditable`

```html
<div contenteditable="true">Editable text</div>
```

An editable element automatically becomes keyboard-focusable and participates in the natural tab sequence.

It behaves similarly to using:

```html
tabindex="0"
```

---

# ⚡ `autofocus`

```html
<input autofocus />
```

The browser automatically moves focus to the element when the page loads.

## Use Carefully

On normal pages, `autofocus` may:

- Disorient screen reader users.
- Cause unexpected scrolling.
- Skip important instructions or labels.

### Recommended Use

Inside an opened `<dialog>`, autofocus is often appropriate for:

- The first form control.
- The primary action.
- The close button.

---

# 🛡️ Disabling Interaction

Several HTML mechanisms restrict interaction, but they serve different purposes.

---

## 1. `tabindex="-1"`

Removes the element from keyboard navigation.

```html
<button tabindex="-1">Hidden from Tab</button>
```

### Limitation

The element:

- Can still be clicked.
- Remains available to assistive technologies (unless otherwise hidden).
- Is **not disabled**.

---

## 2. `disabled`

Applies only to native form controls.

```html
<button disabled>Submit</button>
```

Effects:

- Cannot receive focus.
- Cannot be clicked.
- Is excluded from form submission.
- Matches the `:disabled` pseudo-class.

Supported elements include:

- `<button>`
- `<input>`
- `<select>`
- `<textarea>`
- `<fieldset>`
- `<option>`
- `<optgroup>`

---

## 3. `inert`

The `inert` attribute disables an entire subtree.

```html
<div inert>...</div>
```

Everything inside becomes:

- ❌ Not focusable
- ❌ Not clickable
- ❌ Not selectable
- ❌ Hidden from the accessibility tree

This is especially useful when:

- A modal dialog is open.
- Background content should become inactive.
- Side panels are temporarily disabled.

> **Note:** Modern browsers support `inert`, but very old browsers may require a polyfill.

---

# 🎨 Styling Inert Content

The browser does not visually indicate that content is inert.

Provide your own styling.

```css
[inert] {
  opacity: 0.5;
  pointer-events: none;
  user-select: none;
}
```

This gives users clear visual feedback that the content is currently unavailable.

---

# ✅ Best Practices

- Keep the DOM order aligned with the visual order.
- Test every page using **Tab** and **Shift + Tab**.
- Prefer native HTML controls over custom widgets.
- Use `:focus-visible` instead of removing focus outlines.
- Use `tabindex="0"` only when creating custom interactive components.
- Use `tabindex="-1"` for programmatic focus management.
- Avoid positive `tabindex` values.
- Use `disabled` for form controls.
- Use `inert` to deactivate entire interface regions.
- Use `autofocus` sparingly, primarily inside modal dialogs.

---

# ✅ Key Takeaways

- Keyboard focus is essential for accessibility.
- Visual order should always reflect DOM order.
- CSS reordering should never break keyboard navigation.
- `tabindex="0"` makes custom elements keyboard-focusable.
- `tabindex="-1"` enables programmatic focus without adding the element to the Tab sequence.
- Positive `tabindex` values are considered an accessibility anti-pattern.
- Native controls provide built-in accessibility and should be preferred.
- `disabled` and `inert` solve different problems and are **not interchangeable**.
- Always provide visible focus indicators.
- Test every interface without using a mouse.
