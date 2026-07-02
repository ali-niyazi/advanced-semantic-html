# Module 19: Dialogs & Interactive Modals

## 🧠 Core Philosophy

The HTML `<dialog>` element provides a **native**, **accessible**, and **semantic** way to build:

- Modal dialogs
- Confirmation prompts
- Popups
- Overlay windows

Before `<dialog>`, developers often relied on complex JavaScript to implement:

- Focus trapping
- Backdrop overlays
- Keyboard navigation
- Focus restoration

Modern browsers now provide these behaviors natively, making `<dialog>` the preferred solution for most dialog interfaces.

> **Best Practice:** Use the native `<dialog>` element whenever it meets your UI requirements instead of building custom modal components from scratch.

---

# 🎭 Modal vs. Non-Modal Dialogs

HTML supports two distinct dialog modes.

## Modal Dialog

Open using:

```javascript
dialog.showModal();
```

Characteristics:

- Appears in the browser's **Top Layer**
- Automatically traps keyboard focus
- Makes the rest of the page **inert**
- Displays a native backdrop
- Supports closing with the <kbd>Esc</kbd> key (unless prevented)

Ideal for:

- Confirmation dialogs
- Authentication prompts
- Critical user decisions

---

## Non-Modal Dialog

Open using:

```javascript
dialog.show();
```

or

```html
<dialog open></dialog>
```

Characteristics:

- Does **not** trap focus
- Background remains interactive
- No backdrop is created
- Requires an explicit close mechanism

Suitable for:

- Floating tool palettes
- Inspectors
- Side utilities
- Non-blocking information panels

---

# 🔌 The `HTMLDialogElement` API

Every `<dialog>` exposes a dedicated JavaScript interface.

```javascript
const dialog = document.querySelector("dialog");

dialog.show();

dialog.showModal();

dialog.close();
```

| Method        | Purpose                                                |
| ------------- | ------------------------------------------------------ |
| `show()`      | Opens a non-modal dialog.                              |
| `showModal()` | Opens a modal dialog with focus trapping and backdrop. |
| `close()`     | Closes the dialog.                                     |

---

## `returnValue`

When a dialog closes, its `returnValue` property stores the value associated with the control that dismissed it.

Example:

```html
<button value="confirm">Confirm</button>
```

```javascript
dialog.addEventListener("close", () => {
  console.log(dialog.returnValue);
});
```

This is especially useful for confirmation dialogs.

> **Note:** `returnValue` is typically set via the `value` attribute of the submitting button when using `method="dialog"`.

---

# 🚪 Closing Dialogs Without JavaScript

Dialogs can be closed declaratively using forms.

---

## Form-Level Closing

```html
<dialog>
  <form method="dialog">
    <button>Close</button>
  </form>
</dialog>
```

Submitting the form automatically closes the dialog.

---

## Button-Level Closing

You can override an individual button.

```html
<dialog>
  <form action="/submit" method="post">
    <button type="submit">Save</button>

    <button type="submit" formmethod="dialog" formnovalidate>Cancel</button>
  </form>
</dialog>
```

This allows one button to submit data while another simply dismisses the dialog.

---

# ♿ Accessibility

One of the biggest advantages of `<dialog>` is that browsers implement much of its accessibility automatically.

---

## Focus Management

When a modal dialog opens:

- Focus moves inside the dialog.
- Tab navigation is restricted to dialog contents.
- Background content becomes inaccessible.

When the dialog closes:

- Focus automatically returns to the element that opened it.

This behavior dramatically reduces the amount of JavaScript developers need to write.

---

## `autofocus`

Use `autofocus` to control the initial focus.

```html
<dialog>
  <form method="dialog">
    <p>Please confirm your action.</p>

    <button autofocus>I Understand</button>
  </form>
</dialog>
```

This is often preferable to focusing the first form field, especially when users should read explanatory content first.

---

## Accessible Names

Every dialog should have an accessible name.

Recommended approach:

```html
<dialog aria-labelledby="dialog-title">
  <h2 id="dialog-title">Delete Account?</h2>

  <p>This action cannot be undone.</p>
</dialog>
```

Screen readers announce the dialog title when it opens.

---

## Alert Dialogs

For urgent confirmations requiring immediate attention, use:

```html
<dialog role="alertdialog"></dialog>
```

Examples:

- Permanent deletion
- Security warnings
- Critical errors

Otherwise, the default implicit role of `dialog` is sufficient.

---

## Don't Add `tabindex`

Avoid patterns like:

```html
<dialog tabindex="0"></dialog>
```

The dialog itself is not intended to participate in the normal tab sequence.

Allow the browser to manage focus automatically.

---

# 🎨 Styling Dialogs

Dialogs can be styled like any other HTML element.

```css
dialog {
  border: none;
  border-radius: 12px;
  padding: 2rem;
}
```

---

## Styling the Backdrop

When opened using `showModal()`, the backdrop is available through the `::backdrop` pseudo-element.

```css
dialog::backdrop {
  background: rgb(0 0 0 / 75%);

  backdrop-filter: blur(4px);
}
```

This provides a modern frosted-glass appearance while dimming background content.

---

# 🎯 Best Practices

- Prefer native `<dialog>` over custom modal implementations.
- Use `showModal()` for blocking interactions.
- Use `show()` for non-blocking overlays.
- Always provide a clear close mechanism.
- Give every dialog an accessible name.
- Use `method="dialog"` for simple confirmation dialogs.
- Use `autofocus` thoughtfully to improve usability.
- Style the backdrop using `::backdrop`.
- Let the browser manage focus—avoid custom focus trapping unless absolutely necessary.

---

# ⚠️ Common Pitfalls

❌ Building custom focus traps unnecessarily.

❌ Forgetting an accessible title.

❌ Using `tabindex` on `<dialog>`.

❌ Removing keyboard escape routes.

❌ Replacing the native dialog with complex JavaScript when the native element already provides the required behavior.

---

# ✅ Key Takeaways

- `<dialog>` is the native HTML solution for dialogs and modals.
- `showModal()` creates a modal dialog with automatic focus trapping.
- `show()` creates a non-modal overlay.
- `close()` dismisses the dialog.
- `method="dialog"` enables declarative closing without JavaScript.
- Browsers automatically manage focus movement and restoration.
- Use `aria-labelledby` to provide an accessible name.
- Use `role="alertdialog"` only for urgent interactions.
- Style modal overlays using the `::backdrop` pseudo-element.
- Prefer native dialog behavior over custom modal implementations whenever possible.
