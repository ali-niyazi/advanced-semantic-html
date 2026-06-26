# Module 03: Semantic HTML & Accessibility Architecture

## Core Philosophy

Semantic HTML means using elements to structure content based on their **meaning**, not their appearance. Appearance is strictly the domain of CSS.

- **Div Soup:** Using `<div>` and `<span>` provides zero context to automated tools, search engines, and assistive devices.
- **Semantic Structure:** Using elements like `<header>`, `<main>`, `<section>`, and `<footer>` provides machine-readable architecture and logical outlines.

## The Accessibility Object Model (AOM)

Just as the browser parses HTML to build the DOM (for JavaScript) and the CSSOM (for styling), it simultaneously builds the **Accessibility Tree (AOM)**.

- Assistive technologies (like Screen Readers) rely entirely on the AOM to navigate content.
- Semantic HTML automatically generates **Landmark Roles** in the AOM, enabling keyboard-reliant users to jump swiftly between major sections of a page.

## The `role` Attribute & ARIA

The `role` attribute is a global attribute defined by the ARIA specification.

- Semantic elements have **implicit roles** (e.g., `<main>` is automatically `role="main"`, `<button>` is `role="button"`).
- **The Senior Developer Rule:** Do not reinvent the wheel. While you can technically add `role="button"` to a `<div>`, you lose all native features (tab-indexing, Space/Enter key activation). Always prefer the native semantic element over explicitly assigning roles to non-semantic elements.
