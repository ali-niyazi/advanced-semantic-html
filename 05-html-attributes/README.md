# Module 05: HTML Attributes & State Architecture

## Core Principles

Attributes define the behavior, linkages, and functionality of HTML elements. Understanding how browsers parse different types of attributes is critical for robust web architecture.

## Boolean vs. Enumerated Attributes

- **Boolean Attributes (e.g., `disabled`, `required`):** - Presence implies `true`. Absence implies `false`.
  - Supplying a false value (e.g., `required="false"`) is invalid; the browser still evaluates it as `true`.
  - **JS Best Practice:** Use `removeAttribute('disabled')` and `setAttribute('disabled', '')` to toggle state, never toggle the value string.
- **Enumerated Attributes (e.g., `contenteditable`):** - Accept predefined values (e.g., `true`, `false`).
  - Invalid or missing values default to the attribute's specific default state (often `inherit`).

## ♿ Accessibility (A11y) & The `id` Attribute

- The `id` must be globally unique within the document.
- **Explicit Labels:** Pairing a `<label for="uniqueId">` with an `<input id="uniqueId">` is mandatory for accessible forms. It increases the hit-area for mobile users and provides semantic context for Screen Readers.
- **ARIA Linking:** The `id` is crucial for accessibility relationships like `aria-labelledby`, `aria-describedby`, and `aria-activedescendant`.

## Focus Management (`tabindex`)

- `tabindex="0"`: Adds an element to the natural keyboard tab flow (source code order).
- `tabindex="-1"`: Removes an element from the tab flow but allows it to receive focus programmatically via JavaScript (`element.focus()`).
- **Anti-Pattern:** Never use a `tabindex` greater than `0`. It destroys the natural DOM tab order and creates a confusing experience for keyboard and screen reader users.

## Custom State & `data-*` Attributes

- Custom attributes must begin with `data-` and contain no uppercase letters.
- They provide a standard way to store extra information without hacking the `class` attribute.
- **JavaScript Dataset API:** Browsers map `data-custom-name="value"` to the DOM element's `dataset` object as camelCase (`element.dataset.customName`), allowing highly performant reads and writes without complex DOM queries.
