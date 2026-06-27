# Module 06: Text Basics & Semantic Prose

## Key Takeaways

Typography in HTML is about **meaning**, not presentation. Using the correct elements allows screen readers to navigate content intelligently via the Accessibility Object Model (AOM).

## Semantic Text Elements

- **Headings (<h1>-<h6>):** They provide the document outline for screen readers. **Never skip levels** (e.g., jump from h2 to h4). Browsers' default font sizes for headings are just defaults; use CSS for actual styling.
- **Paragraphs (<p>):** Use `<p>` for blocks of text. Never use `<br>` to separate paragraphs; `<br>` is strictly for line breaks within addresses, poetry, or signatures.
- **Quotes & Citations:**
  - `<blockquote>`: For block-level quotes.
  - `<q>`: For inline quotes (the browser adds quotes automatically based on `lang`).
  - `<cite>`: For the **title** of a work/source (not the author).
  - `cite attribute`: Used on `<q>` or `<blockquote>` to provide a machine-readable source URL.

## Accessibility Hacks

- **Landmarks:** `<section>` is not a landmark by default. It becomes one if it has an accessible name, usually via `aria-labelledby` referencing an ID on a heading.
- **Language Awareness:** Use the `lang` attribute (e.g., `lang="fr"`) on elements containing foreign text to ensure screen readers use the correct pronunciation engine.

## HTML Entities

- Reserve characters (`<`, `>`, `&`, `"`) must be escaped using entities (e.g., `&lt;`) to prevent rendering issues.
- With `UTF-8` character encoding declared in the `<head>`, most other characters (including emojis) can be written directly without needing entity codes.
