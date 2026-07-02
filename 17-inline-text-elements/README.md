# Module 17: Other Inline Text Elements & Text Semantics

## 🧠 Core Philosophy

HTML is a **semantic language**, not merely a markup language for styling text.

Inline text elements communicate meaning to:

- Browsers
- Screen readers
- Search engines
- Translation tools
- Other software consuming HTML

Choose elements based on **what the content means**, not **how it should look**.

> **Rule of Thumb:** If your choice is driven only by appearance, use CSS—not a semantic HTML element.

---

# 💻 Technical Writing & Code Representation

HTML provides several elements specifically designed for technical documentation.

## `<code>`

Represents a short inline code fragment.

```html
Press <code>Ctrl + C</code> to copy.
```

By default, browsers render `<code>` using a monospace font.

---

## `<pre>`

Represents **preformatted text**.

Whitespace and line breaks are preserved exactly as written.

To display multiline code, always combine it with `<code>`.

```html
<pre><code>function greet() {
  console.log("Hello, world!");
}</code></pre>
```

---

## `<samp>`

Represents sample output produced by a computer program.

```html
<samp>Compilation completed successfully.</samp>
```

---

## `<kbd>`

Represents user input.

Usually keyboard shortcuts, but it can also represent voice commands or button presses.

```html
Press <kbd>Ctrl</kbd> + <kbd>S</kbd>.
```

---

## `<var>`

Represents:

- Mathematical variables
- Programming placeholders
- User-defined values

```html
<var>x</var> + <var>y</var> = 10
```

Browsers typically render `<var>` in italics.

---

# ⏱️ Machine-Readable Data

Some text is intended for humans, while machines require standardized values.

HTML provides dedicated semantic elements for these cases.

---

## `<data>`

Associates human-readable text with a machine-readable value.

```html
<p>
  Our top model is

  <data value="PRO-9000"> Super Fast Pro </data>
</p>
```

Useful for:

- Product identifiers
- SKU numbers
- Internal database IDs

---

## `<time>`

Represents dates or times.

Always provide a machine-readable value using the `datetime` attribute.

```html
<p>
  The workshop starts on

  <time datetime="2026-07-02T19:30"> July 2, 2026 at 7:30 PM </time>
</p>
```

### Best Practice

Use **ISO 8601** inside `datetime`.

Benefits include:

- Better SEO
- Calendar integration
- Improved machine readability

---

# 🔄 Document Revisions

HTML includes dedicated elements for tracking edits.

---

## `<del>`

Marks deleted content.

```html
<del datetime="2026-07-01"> Old price </del>
```

Optional attributes:

- `datetime`
- `cite`

---

## `<ins>`

Marks inserted content.

```html
<ins datetime="2026-07-02"> New price </ins>
```

Supports:

- `datetime`
- `cite`

---

## `<s>`

Represents content that is **no longer accurate**, but remains part of the document.

Example:

```html
<s>$199</s>

$149
```

Unlike `<del>`, the content has **not been removed**—it has simply become outdated.

---

# 🌍 Definitions & Internationalization

---

## `<abbr>`

Represents abbreviations or acronyms.

Provide the expanded form using the `title` attribute.

```html
<abbr title="HyperText Markup Language"> HTML </abbr>
```

Best practice:

- Spell out the full term on first use.
- Use the abbreviation afterward.

---

## `<dfn>`

Marks the defining occurrence of a term.

```html
<p>
  <dfn>Semantic HTML</dfn>

  is HTML that conveys meaning.
</p>
```

---

## `<bdi>`

**Bidirectional Isolation**

Useful when inserting user-generated text with an unknown writing direction.

```html
<bdi>محمد</bdi>
```

Prevents surrounding text from becoming directionally corrupted.

Common use cases:

- Usernames
- Comments
- Chat messages

---

## `<bdo>`

**Bidirectional Override**

Explicitly forces text direction.

```html
<bdo dir="rtl"> Hello </bdo>
```

Use only when intentional direction overriding is required.

---

## `<ruby>`

Provides pronunciation annotations (commonly used in Japanese and Chinese typography).

```html
<ruby>
  漢

  <rt>かん</rt>

  <rp>(</rp>
  <rp>)</rp>
</ruby>
```

Elements:

| Element  | Purpose                                 |
| -------- | --------------------------------------- |
| `<ruby>` | Annotation container                    |
| `<rt>`   | Pronunciation text                      |
| `<rp>`   | Fallback parentheses for older browsers |

---

# 📢 Emphasis & Text Semantics

Choose elements according to meaning—not appearance.

---

## `<em>`

Indicates stress emphasis.

```html
You <em>must</em> read this.
```

Screen readers often change pronunciation to reflect emphasis.

---

## `<strong>`

Represents strong importance, seriousness, or urgency.

```html
<strong>Warning:</strong>

Do not unplug the device.
```

---

## `<mark>`

Highlights text relevant to the user's current task.

Common example:

- Search result highlighting

```html
<mark>Accessibility</mark>
```

Unlike `<strong>`, it does **not** indicate importance.

---

## `<cite>`

Represents the title of a creative work.

Examples include:

- Books
- Movies
- Research papers
- Paintings
- Songs

```html
<cite>The Pragmatic Programmer</cite>
```

> **Note:** `<cite>` is for the **title** of a work—not the author's name.

---

## `<i>`

Represents text that differs from surrounding prose without conveying emphasis.

Examples:

- Scientific names
- Technical terms
- Foreign words
- Internal thoughts

```html
<i>Homo sapiens</i>
```

Do **not** use `<i>` merely to italicize text.

---

## `<u>`

Represents non-textual annotations.

Typical use:

- Indicating a spelling error.

```html
<u>recieve</u>
```

Avoid using `<u>` solely because you want underlined text.

---

## `<b>`

Draws attention to text without adding semantic importance.

Examples:

- Keywords
- Product names
- Lead-in phrases

```html
<b>Important:</b>
```

If the text is actually important, prefer:

```html
<strong></strong>
```

instead.

---

# 💨 Whitespace & Structural Breaks

---

## `<br>`

Represents a line break.

Appropriate for:

- Poetry
- Postal addresses
- Song lyrics

```html
123 Main Street<br />
New York, NY
```

Do **not** use `<br>` to create vertical spacing.

Use CSS margins instead.

---

## `<hr>`

Represents a thematic break between sections.

```html
<hr />
```

Modern HTML treats `<hr>` as a semantic separator—not merely a horizontal line.

---

## `<wbr>`

Represents a possible word-break opportunity.

Useful for extremely long strings.

```html
https://example.com/very<wbr />long<wbr />url
```

The browser may wrap the line here if needed without inserting a hyphen.

---

# ✅ Best Practices

- Choose semantic elements based on meaning, not appearance.
- Use CSS for presentation.
- Wrap multiline code with `<pre><code>`.
- Prefer `<kbd>` for user input and `<samp>` for program output.
- Use `<time>` with ISO 8601 dates.
- Use `<abbr>` with the `title` attribute.
- Use `<strong>` for importance and `<em>` for emphasis.
- Use `<mark>` only for contextually relevant highlights.
- Prefer `<bdi>` when displaying unknown user-generated text directions.
- Use `<wbr>` to improve readability of long strings.

---

# ✅ Key Takeaways

- HTML contains rich inline semantics beyond basic formatting.
- `<code>`, `<kbd>`, `<samp>`, and `<var>` improve technical documentation.
- `<data>` and `<time>` provide machine-readable information.
- `<del>`, `<ins>`, and `<s>` represent different kinds of document changes.
- `<abbr>`, `<dfn>`, `<bdi>`, `<bdo>`, and `<ruby>` improve clarity and internationalization.
- `<em>` and `<strong>` communicate meaning—not visual style.
- `<mark>` highlights relevance rather than importance.
- `<cite>` identifies the title of a creative work.
- `<br>`, `<hr>`, and `<wbr>` each have distinct semantic purposes.
