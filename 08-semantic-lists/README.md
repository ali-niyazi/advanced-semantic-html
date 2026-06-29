# Module 08: Semantic Lists & Structural Grouping

## Core Philosophy

Lists represent semantic collections of related items. HTML provides three distinct structures to mark up collections: Unordered (`<ul>`), Ordered (`<ol>`), and Description (`<dl>`) lists. Choosing the right list type provides essential context to search engines, browsers, and assistive technologies.

## The VoiceOver & CSS Layout Bug (A11y Critical)

- **The Issue:** When CSS removes default list styles (e.g., `list-style: none`, `display: flex`, or `display: grid`), Safari on iOS/macOS strips the implicit semantic `list` role from `<ul>` and `<ol>` in the Accessibility Object Model (AOM).
- **The Solution:** If the collection size is beneficial for screen reader users to know, explicitly restore the semantic role using ARIA:

  ```html
  <ul role="list" class="navigation-bar">
    <li><a href="#reg">Register</a></li>
  </ul>
  ```

## Listing Rules & Nesting Laws

1. **Direct Children:** The only valid direct child of a `<ul>` or `<ol>` is `<li>`. Putting other elements directly inside a list container violates the HTML standard.
2. **Nesting Lists:** To nest a sub-list, it must be embedded _inside_ an `<li>` element, never directly as a sibling to another `<li>` under the parent list.

   ```html
   <ul>
     <li>
       Parent Item
       <ul>
         <li>Nested Child</li>
       </ul>
     </li>
   </ul>
   ```

## Ordered List Control Attributes

- `type`: Defines the numbering system (`1` for decimal, `a`/`A` for alphabetical, `i`/`I` for roman numerals).
- `start`: Defines the starting integer value of the first list item.
- `reversed`: A boolean attribute that reverses the sequential numbering.
- `value` (on `<li>`): Overrides the default sequential counter on a specific list item within an `<ol>`.

## Description Lists (`<dl>`)

- Represents key-value pairings (formerly known as "Definition Lists").
- Consists of `<dt>` (Description Term) and `<dd>` (Description Details).
- **Modern HTML5 Standard:** You are permitted to wrap `<dt>` and `<dd>` pairs inside `<div>` elements within a `<dl>` to aid CSS layout design (e.g., Grid or Flexbox styling).
