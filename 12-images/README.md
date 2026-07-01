# Module 12: Images, Responsive Graphics, & Alt Text Engineering

## 🧠 Core Philosophy

Images on the web fall into **two distinct categories**:

| Type                  | Usage                                                                                                  |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| **Decorative Images** | Background gradients, patterns, decorative icons, and purely visual assets. These belong in **CSS**.   |
| **Content Images**    | Images that convey information or context. These must be embedded using HTML (`<img>` or `<picture>`). |

---

# 🖼️ The Core Image Element (`<img>`)

A foreground image requires two essential attributes:

- `src` → Image source
- `alt` → Alternative text for accessibility

```html
<img src="images/profile.jpg" alt="Jane Doe smiling in a blue suit" />
```

---

# ♿ The VoiceOver SVG Bug

When SVG files are embedded using `<img>`, **VoiceOver** (iOS/macOS) may occasionally fail to recognize the image or announce its alternative text correctly.

### Solution

Explicitly add `role="img"`.

```html
<img src="switch.svg" alt="Light switch" role="img" />
```

---

# ✍️ Alt Text Engineering (Accessibility Critical)

Good alt text is **not** a literal visual description.

Its purpose is to communicate the **same information, meaning, or humor** to someone who cannot see the image.

---

## 1. Context Dictates Content

The same image can require completely different alt text depending on context.

### Avatar Context

```text
alt="Fluffy"
```

If the image appears beside a user's comment on a pet forum, simply identifying the dog is enough.

### Adoption Context

```text
alt="Fluffy, a tri-color terrier with short hair, holding a tennis ball in her mouth"
```

On an adoption website, users need descriptive information.

---

## 2. General Alt Text Rules

### ✅ Avoid Redundancy

Don't write:

```text
Photo of...
Image of...
Picture of...
```

Screen readers already announce that the element is an image.

---

### ✅ Describe Function, Not Appearance

Icons should communicate **their purpose**, not their shape.

| ❌ Don't           | ✅ Do    |
| ------------------ | -------- |
| "Magnifying glass" | "Search" |
| "Floppy disk"      | "Save"   |
| "Trash can"        | "Delete" |

---

### ✅ Decorative Images

Decorative images should remain in the markup only if necessary.

Use an empty alt attribute and remove them from the accessibility tree.

```html
<img src="svg/divider.svg" alt="" role="none" />
```

---

# ⚡ Responsive Images

Large desktop images shouldn't be downloaded on small mobile devices.

HTML provides two major responsive image techniques.

---

## 1. Resolution Switching (`srcset` + `sizes`)

Allows the browser to choose the most appropriate image based on viewport width and screen density.

```html
<img
  src="images/photo.jpg"
  alt="Landscape"
  srcset="images/photo-sm.jpg 400w, images/photo-xl.jpg 800w"
  sizes="
    (max-width: 800px) 400px,
    800px"
/>
```

---

## 2. Art Direction & Modern Formats (`<picture>`)

Use `<picture>` when:

- Mobile requires a different crop.
- Different image formats should be served (AVIF, WebP).
- A fallback image is needed.

```html
<picture>
  <source
    srcset="images/hero-mobile.webp"
    media="(max-width: 600px)"
    type="image/webp"
  />

  <source srcset="images/hero-desktop.jpg" />

  <img src="images/hero-fallback.jpg" alt="Workshop banner" />
</picture>
```

---

# 🚀 Performance Optimization & Layout Shift (CLS)

## 1. Prevent Cumulative Layout Shift (CLS)

Browsers don't know an image's dimensions until it loads.

Without reserved space, surrounding content shifts downward, harming Core Web Vitals.

### Solution

Always provide **unitless** `width` and `height`.

```html
<img src="avatar.jpg" alt="Avatar" width="300" height="400" />
```

The browser can immediately reserve the correct aspect ratio while CSS still allows responsive resizing.

---

## 2. Native Lazy Loading

Delay loading images that are off-screen.

```html
<img src="footer-image.jpg" alt="Partners" loading="lazy" />
```

### Best Practice

✅ Lazy-load:

- Gallery images
- Footer graphics
- Images below the fold

❌ Do **not** lazy-load:

- Hero banners
- Above-the-fold images
- Largest Contentful Paint (LCP) elements

Lazy-loading critical images delays rendering and negatively impacts performance.

---

# ✅ Key Takeaways

- Use **CSS** for decorative images and **HTML** for content images.
- Every content image needs meaningful **alt** text.
- Alt text should communicate **purpose**, not appearance.
- Use `role="img"` when necessary for SVG accessibility.
- Use `srcset` and `sizes` for responsive resolution switching.
- Use `<picture>` for art direction and modern image formats.
- Always specify `width` and `height` to prevent CLS.
- Lazy-load only non-critical, off-screen images.
