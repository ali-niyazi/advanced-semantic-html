# Module 09: Navigation Architecture & Accessibility

## Core Philosophy

Navigation is the spatial awareness system of the web. It tells users and search engine crawlers where they are, where they can go, and how the site is structured. Proper semantic markup is essential for a predictable and accessible user journey.

## The `<nav>` Landmark

- The `<nav>` element automatically creates a "navigation" landmark in the Accessibility Object Model (AOM).

- **Anti-pattern:** Never use `aria-label="Navigation"` on a `<nav>`. Screen readers already announce it as "navigation" (resulting in "Navigation navigation"). If you have multiple `<nav>` elements, distinguish them properly (e.g., `aria-label="Primary"`, `aria-label="Breadcrumbs"`).

- **Pro Tip:** Use `aria-labelledby` to link the `<nav>` to a visible heading (like a "Table of Contents" title) for better internationalization, as translation services translate visible text but often ignore attribute values.

## Skip to Content Links

- A critical A11y requirement. It allows keyboard-only users to bypass massive global navigation blocks and jump straight to the `<main>` content.

- **Implementation:** `<a href="#main" class="skip-link">Skip to main</a>`.

- **CSS Strategy:** Hide it visually until it receives focus. When a user presses the `Tab` key, it should become fully visible.

## Breadcrumb Navigation

- Represents the hierarchical path (URL structure or logical structure) to the current page.

- **Markup:** Use an Ordered List (`<ol role="list">`) because the hierarchy is strictly sequential.

- **Separators:** Use CSS pseudo-elements (`::before`/`::after`) for the slashes or arrows between breadcrumbs. Never put separator characters directly in the HTML text, as screen readers will read them aloud out of context.

- **Current Page:** The active/current page should always be marked with the attribute `aria-current="page"`.

## Global vs. Local Navigation

- **Global Navigation:** Consistent across the entire site (e.g., top header bar, site footer). It should look and behave predictably on every page.

- **Local Navigation:** Specific to the current section or page (e.g., Table of Contents, sidebar filters).

- **Predictability Rule:** Tab order and navigation placement should remain logical and consistent even when the layout shifts responsively for smaller viewports.
