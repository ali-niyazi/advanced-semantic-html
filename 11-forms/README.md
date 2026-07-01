# Module 11: Web Forms & Native Constraint Validation

## 🧠 Core Philosophy

The HTML `<form>` element is a powerhouse. It represents a document landmark containing interactive controls.

Understanding how to leverage native HTML attributes for validation, keyboard optimization, and accessibility separates senior developers from those who over-rely on heavy JavaScript libraries.

---

## 🔌 Submission, Actions & Overrides

### HTTP Methods

| Method     | Description                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| **GET**    | Appends form data to the URL as query parameters (`?name=value`). **Never use this for sensitive data.**                 |
| **POST**   | Sends form data in the body of the HTTP request. **Mandatory for passwords, payment details, and other sensitive data.** |
| **DIALOG** | Closes a `<dialog>` via `<form method="dialog">` without clearing or submitting data.                                    |

### Declarative Overrides

Submit buttons can override their parent `<form>` attributes using:

| Attribute        | Purpose                                                                                 |
| ---------------- | --------------------------------------------------------------------------------------- |
| `formaction`     | Submits the form to a different URL.                                                    |
| `formmethod`     | Uses a different HTTP method (e.g., `POST` instead of `GET`).                           |
| `formnovalidate` | Bypasses client-side validation. Useful for **Save Draft** or **Close Dialog** buttons. |

---

## 🏷️ Accessible Labeling & Structural Grouping

### Accessible Name (A11y)

Every form control **must** have an associated `<label>`.

#### Explicit Label (Recommended)

```html
<label for="username">Username</label> <input id="username" />
```

- Preferred for precise styling.
- Most flexible and explicit.

#### Implicit Label

```html
<label>
  Username
  <input />
</label>
```

- Creates a naturally larger click/tap target.
- Useful for simpler layouts.

### ❌ Interactive Nesting Violation

Never place other interactive elements (such as `<a>` links or `<button>`) inside a `<label>`.

Doing so:

- Confuses assistive technologies.
- Breaks click propagation.
- Creates inconsistent user interactions.

### Grouping Related Controls

Use:

- `<fieldset>` → Groups related form controls.
- `<legend>` → Provides the accessible name for the group.

Example:

```html
<fieldset>
  <legend>Payment Method</legend>

  <label>
    <input type="radio" name="payment" />
    Credit Card
  </label>

  <label>
    <input type="radio" name="payment" />
    PayPal
  </label>
</fieldset>
```

> **Note:** Disabling a `<fieldset>` automatically disables all nested controls.

---

## 📱 Input Types & Dynamic Keyboards

Choosing the correct `type` improves the keyboard shown on mobile devices.

| Input Type     | Mobile Keyboard                  |
| -------------- | -------------------------------- |
| `type="tel"`   | Numeric telephone keypad         |
| `type="email"` | Includes `@` and `.` keys        |
| `type="url"`   | Optimized with `/`, `.com`, etc. |

### Media Capture

```html
<input type="file" accept="image/*" capture="user" />
```

On supported mobile devices, this directly opens the **front-facing camera**.

---

## 🛡️ Built-in Constraint Validation (Zero JavaScript)

HTML provides powerful native validation using built-in attributes.

### Common Validation Attributes

| Attribute                 | Purpose                                             |
| ------------------------- | --------------------------------------------------- |
| `required`                | Prevents empty submissions.                         |
| `pattern`                 | Validates input using a Regular Expression (RegEx). |
| `min` / `max` / `step`    | Restricts numeric, date, or time values.            |
| `minlength` / `maxlength` | Restricts character count.                          |

### Native Validation Flow

When the user submits the form:

1. The browser checks every validation constraint.
2. If any constraint fails:
   - Submission is blocked.
   - Focus moves to the first invalid field.
   - A built-in validation message is displayed.

Common validity states include:

- `valueMissing`
- `typeMismatch`
- `patternMismatch`
- `rangeOverflow`
- `rangeUnderflow`
- `tooShort`
- `tooLong`
- `stepMismatch`

---

## 🎨 CSS UI Pseudo-classes

Style form controls dynamically using:

```css
:required
:optional
:valid
:invalid
:in-range
:out-of-range
```

Example:

```css
input:valid {
  border-color: green;
}

input:invalid {
  border-color: red;
}
```

---

## ⚠️ Anti-pattern Warning

**Do not disable the submit button** using CSS like:

```css
form:invalid button {
  pointer-events: none;
}
```

### Why?

If users cannot click **Submit**, they cannot trigger the browser's native validation UI, making it harder to understand what needs fixing.

✅ **Best Practice:**

Always allow the user to click **Submit**, so native constraint validation can:

- Block the submission.
- Focus the first invalid field.
- Display helpful browser validation messages automatically.
