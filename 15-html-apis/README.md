# Module 15: HTML Element APIs, DOM, and Window Architecture

## 🧠 Core Philosophy

HTML elements are not merely text tags—they become **Element Nodes** within the **Document Object Model (DOM)**. Along with text nodes, comment nodes, and the document node itself, they form a tree of JavaScript objects. Every node exposes native properties, methods, and events, allowing developers to programmatically inspect and manipulate the page, media, and browser environment.

---

# 🌳 DOM vs. Accessibility Tree (AOM)

## Document Object Model (DOM)

The DOM is a programmable tree representing the structure of a document.

It contains every node in the document, including:

- Elements
- Attributes
- Text nodes
- Comment nodes
- Document node

JavaScript interacts with the page through this tree.

## Accessibility Tree

Browsers generate a separate **Accessibility Tree** from the DOM using semantic HTML and ARIA attributes.

This tree is consumed by assistive technologies such as:

- Screen Readers
- Voice Assistants
- Other accessibility tools

The **Accessibility Object Model (AOM)** is an emerging API intended to expose and interact with this accessibility information programmatically.

---

# 🧬 Interface Inheritance Hierarchy

HTML elements inherit functionality through a chain of interfaces:

```text
EventTarget
   └── Node
        └── Element
             └── HTMLElement
                  └── HTMLImageElement
```

Each layer contributes additional capabilities:

| Interface            | Adds                                                                 |
| -------------------- | -------------------------------------------------------------------- |
| **EventTarget**      | `addEventListener()`, `removeEventListener()`                        |
| **Node**             | `firstChild`, `nextSibling`, `appendChild()`, `cloneNode()`          |
| **Element**          | `attachShadow()`, attribute manipulation, DOM traversal capabilities |
| **HTMLElement**      | `offsetHeight`, `style`, `hidden`, focus management                  |
| **HTMLImageElement** | `alt`, `src`, `srcset`, `naturalWidth`, `naturalHeight`              |

> **Note:** Methods such as `querySelector()` and `querySelectorAll()` are available on `Element`, `Document`, and `DocumentFragment` through the **ParentNode** mixin rather than being exclusive to `Element`.

---

# 📋 Specialized HTML Interfaces

Many HTML elements expose specialized JavaScript APIs.

Some common examples include:

| Element              | Interface           | Common APIs                                                       |
| -------------------- | ------------------- | ----------------------------------------------------------------- |
| `<img>`              | `HTMLImageElement`  | `alt`, `src`, `srcset`                                            |
| `<audio>`, `<video>` | `HTMLMediaElement`  | `duration`, `currentTime`, `paused`, `ended`, `play()`, `pause()` |
| `<dialog>`           | `HTMLDialogElement` | `show()`, `showModal()`, `close()`                                |
| `<form>`             | `HTMLFormElement`   | `submit()`, `reset()`, validation APIs                            |

Many structural elements—including:

- `<section>`
- `<article>`
- `<nav>`
- `<header>`
- `<footer>`
- `<aside>`

do **not** expose additional specialized APIs beyond those inherited from `HTMLElement`.

---

# 🔄 Property Overriding

Child interfaces may redefine inherited properties.

Example:

- `HTMLCollection.length` is **read-only**.
- `HTMLOptionsCollection.length` (returned by `HTMLSelectElement.options`) is **read/write**, allowing JavaScript to change the number of `<option>` elements programmatically.

The child interface overrides the inherited behavior.

---

# 🌲 Traversing the DOM Tree

The `Node` interface provides relationships for navigating the DOM:

- `firstChild`
- `lastChild`
- `nextSibling`
- `previousSibling`
- `parentNode`

A classic recursive DOM traversal algorithm by Douglas Crockford:

```javascript
const walk_the_DOM = function walk(node, callback) {
  callback(node);
  node = node.firstChild;
  while (node) {
    walk(node, callback);
    node = node.nextSibling;
  }
};
```

Useful methods inherited from `Node` include:

- `appendChild()`
- `removeChild()`
- `replaceChild()`
- `cloneNode()`

---

# 📄 Document Interface

The global `document` object represents the currently loaded document.

It inherits from `Node`.

Historically browsers exposed `HTMLDocument`, but modern browsers simply expose a `Document` object for HTML pages.

Common APIs include:

### Document Collections

```javascript
document.body;
document.head;
document.styleSheets;
document.forms;
document.images;
```

### Document Metadata

```javascript
document.location;
document.lastModified;
document.cookie;
```

> Although `document.location` is supported, `window.location` is the more commonly used and standardized interface.

The Document interface also participates in browser features such as:

- Drag and Drop
- Fullscreen API

through document-level methods and events.

---

# 🪟 Window Interface

`window` represents the global execution context of the current browsing context (such as a browser tab, popup window, or iframe).

Every browsing context has its own `Window` object.

It provides access to:

## Browser Information

```javascript
window.devicePixelRatio;
window.innerWidth;
window.innerHeight;
window.location;
```

## Browser Control

```javascript
window.resizeTo();
window.scrollTo();
```

> Modern browsers often restrict `resizeTo()` unless the window was opened via JavaScript (for example, a popup).

## Web Platform APIs

The `Window` interface exposes entry points for many browser APIs, including:

- Web Workers
- IndexedDB
- Local Storage (`window.localStorage`)
- Session Storage (`window.sessionStorage`)
- Fetch API
- Timers (`setTimeout()`, `setInterval()`)

---

# ✅ Key Takeaways

- HTML elements become programmable JavaScript objects inside the DOM.
- Every node inherits functionality through the chain: `EventTarget → Node → Element → HTMLElement`.
- Specialized elements (images, media, forms, dialogs, etc.) expose additional interfaces and APIs.
- The browser generates an independent Accessibility Tree for assistive technologies.
- `Node` provides tree navigation and DOM manipulation methods.
- `Document` represents the loaded document, while `Window` represents the browser's execution environment.
- Understanding these APIs is essential for writing modern, interactive web applications.
