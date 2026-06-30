# Module 10: Tables & Tabular Data

## Core Philosophy

Tables are for **tabular data** only. If you need to present, compare, sort, or calculate data, use a `<table>`. If you are just trying to organize visual elements (like thumbnails), use a list and CSS Grid/Flexbox instead. **Never use tables for layout.**

## Table Hierarchy

The semantic order of elements within a table is crucial:

1. `<table>`: The wrapper. Role is `table` (or `grid`/`treegrid` for interactive data).

2. `<caption>`: The title (must be the first child).

3. `<colgroup>`/`<col>`: Used for column styling hooks.

4. `<thead>`, `<tbody>`, `<tfoot>`: Sectioning elements (each has the role `rowgroup`).

5. `<tr>`: Table row.

6. `<th>` / `<td>`: Header cell vs. Data cell.

## Accessibility & Usability

- **Headers:** Use `<th>` for headers. Browsers apply bold/center by default, but always use CSS for styling.

- **Scope:** Use `scope="col"` or `scope="row"` on `<th>` elements to explicitly associate data with headers. This is vital for screen readers when headers scroll out of view.

- **Complex Tables:** For merged cells, use `colspan` (horizontal merge) and `rowspan` (vertical merge). If the structure is complex, use the `headers` attribute to map cells to their respective `id`s of header cells.

- **Captioning:** Always use `<caption>` as the first child of the `<table>` to provide an immediate context for what the data represents.

## Table Styling (CSS)

- **Border Collapse:** Use `border-collapse: collapse;` on the `<table>` to avoid double borders between cells.

- **Spacing:** Use `border-spacing` for tables with separate borders.

- **Striping:** Use `tbody tr:nth-of-type(odd)` to create "zebra-striping" for better readability.

- **Responsive Tables:** Tables are not responsive by default. Use CSS media queries or overflow wrappers to handle narrow viewports.

## The "Layout Table" Anti-pattern

Using `<table>` for structural page layout is an accessibility disaster. If you are forced to use a table for legacy layout reasons, set `role="none"` on the `<table>` element to strip its semantic meaning and inform assistive technologies that it is not a data table.
