# Module 13: Audio, Video, & Media Accessibility

## 🧠 Core Philosophy

Embedding media with HTML (`<audio>` and `<video>`) requires balancing:

- **Performance**
- **Browser compatibility**
- **Accessibility**

Modern HTML provides native media players and timed text support, eliminating much of the historical need for Flash players or complex JavaScript media libraries.

---

# 📹 Native Media Elements

Both `<audio>` and `<video>` support multiple source files through nested `<source>` elements.

---

## 1. Simple Implementation

For a single media source:

```html
<video src="videos/machines.webm" poster="images/machine.jpg" controls>
  <p>
    Your browser does not support HTML video. Watch the
    <a href="https://youtube.com/link">video on YouTube</a>.
  </p>
</video>
```

### Best Practice

Always include **fallback content** inside the media element.

If the browser cannot play the media, users will still receive useful content.

---

## 2. Robust Multi-Source Implementation

Provide multiple media formats for maximum browser compatibility.

```html
<video controls poster="images/machine.jpg" width="1920" height="1080">
  <source src="videos/machines.webm" type="video/webm;codecs=vp8,vorbis" />

  <source src="videos/machines.mp4" type="video/mp4;codecs=avc1.4d002a" />

  <p>
    Watch
    <a href="https://youtube.com/link"> video on YouTube </a>
  </p>
</video>
```

### Why use multiple sources?

| Feature            | Purpose                                                        |
| ------------------ | -------------------------------------------------------------- |
| `type`             | Prevents browsers from downloading media they cannot decode.   |
| `codecs`           | Specifies the compression algorithm (VP8, Vorbis, AVC, etc.).  |
| `width` & `height` | Reserve layout space to prevent Cumulative Layout Shift (CLS). |

---

# ♿ Timed Text Tracks (`<track>` & WebVTT)

Timed text makes media accessible for:

- Deaf and hard-of-hearing users
- Blind or low-vision users
- Users in noisy environments
- Users in quiet environments

Tracks reference **WebVTT (`.vtt`)** files.

```html
<video controls poster="images/machine.jpg">
  <source src="videos/machines.mp4" type="video/mp4" />

  <track
    label="English"
    kind="subtitles"
    srclang="en"
    src="vtt/subtitles-en.vtt"
    default
  />

  <track
    label="Français"
    kind="subtitles"
    srclang="fr"
    src="vtt/subtitles-fr.vtt"
  />
</video>
```

---

## The Five Track Types

| `kind`         | Purpose                                                       |
| -------------- | ------------------------------------------------------------- |
| `subtitles`    | Speech transcription and translation.                         |
| `captions`     | Includes dialogue, sound effects, and speaker identification. |
| `descriptions` | Describes important visual events for screen readers.         |
| `chapters`     | Navigation through chapter markers.                           |
| `metadata`     | Script-readable timed data.                                   |

---

## Styling Subtitles

Subtitle appearance can be customized using:

```css
::cue

::cue(...)
```

---

# 🚫 Background Videos & Accessibility

Decorative looping background videos introduce both accessibility and performance concerns.

```html
<video playsinline autoplay loop muted poster="images/machine.jpg" role="none">
  <source src="videos/machines.webm" type="video/webm" />

  <source src="videos/machines.mp4" type="video/mp4" />
</video>
```

### Best Practices

### Decorative Media

If the video has no informational value:

```html
role="none"
```

This removes it from the accessibility tree.

---

### Remove Audio

If the background video is always muted:

- Remove the audio track entirely.
- Reduce download size.
- Save bandwidth.

---

### The 5-Second Rule

According to WCAG:

- Media playing longer than **5 seconds**
- must provide a mechanism to **pause**, **stop**, or **hide** playback.

Avoid endlessly looping videos without a pause control.

---

# 🛠️ Custom Media Controls

If creating custom playback controls:

**Never remove native controls immediately.**

Instead, use **Progressive Enhancement**.

---

## Step 1 — Render Native Controls

```html
<audio id="audioElement" controls src="audio/track.mp3"></audio>

<button
  id="playPause"
  aria-controls="audioElement"
  data-pause-text="Pause Audio"
  data-play-text="Play Audio"
>
  Play Audio
</button>
```

---

## Step 2 — Enhance with JavaScript

```javascript
const playButton = document.getElementById("playPause");

playButton.addEventListener("click", togglePlayback);

function togglePlayback() {
  const media = document.getElementById(this.getAttribute("aria-controls"));

  if (media.paused) {
    media.play();
    this.innerText = this.dataset.pauseText;
  } else {
    media.pause();
    this.innerText = this.dataset.playText;
  }
}

// Remove native controls only AFTER JavaScript initializes
document.getElementById("audioElement").removeAttribute("controls");
```

---

# ✅ Progressive Enhancement Workflow

1. Render native HTML controls.
2. Verify JavaScript is available.
3. Initialize custom controls.
4. Remove native controls programmatically.
5. Keep the media accessible even if JavaScript fails.

---

# ✅ Key Takeaways

- Always provide fallback content inside `<audio>` and `<video>`.
- Use multiple `<source>` elements for browser compatibility.
- Include `type` and `codecs` whenever possible.
- Specify `width` and `height` to prevent CLS.
- Use `<track>` with WebVTT files for accessibility.
- Choose the appropriate `kind` (`captions`, `subtitles`, `descriptions`, etc.).
- Decorative videos should use `role="none"`.
- Remove unused audio tracks from muted background videos.
- Videos longer than **5 seconds** should provide a pause mechanism.
- Build custom controls using **Progressive Enhancement**, not replacement-first.
