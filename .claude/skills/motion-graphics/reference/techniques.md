# Techniques Reference

Long-form notes on the 12 named techniques. SKILL.md gives the recipe; this file covers edge cases, when techniques conflict, and CSS-vs-GSAP alternatives.

---

## 1. Radial wipe (stroke-end animation)

The dial filling from 0 to 80% in Scene 1.

### Math

For an SVG circle with `r=80`, circumference = `2 * Math.PI * 80 ≈ 502.65`. To show 80% fill:

```js
const C = 2 * Math.PI * 80; // 502.65
circle.style.strokeDasharray = C;
circle.style.strokeDashoffset = C; // start: fully empty
gsap.to(circle, {
  strokeDashoffset: C * (1 - 0.80), // end: 80% filled
  duration: 1.2,
  ease: "power2.out",
});
```

### Edge cases

- **Counter-clockwise fill:** flip with `transform: scaleX(-1)` on the SVG, or animate `stroke-dashoffset` from negative.
- **Anti-aliasing flicker:** add `shape-rendering="geometricPrecision"` to the circle.
- **Gradient stroke:** define a `<linearGradient>` and reference via `stroke="url(#grad)"`. The animation works the same way.

### CSS alternative

```css
@keyframes draw { to { stroke-dashoffset: 100.53; } }
.dial { animation: draw 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
```

GSAP is preferred because the timeline coordinates with sibling tweens — CSS keyframes don't.

---

## 2. Trim path (line-drawing animation)

The graph line in Scene 1.

### Get the path length

```js
const path = document.querySelector("#graph-line");
const len = path.getTotalLength();
path.style.strokeDasharray = len;
path.style.strokeDashoffset = len;
gsap.to(path, { strokeDashoffset: 0, duration: 1.5, ease: "power2.inOut" });
```

`getTotalLength()` works on `<path>`, `<line>`, `<polyline>`, `<rect>`, `<circle>`. For a `<rect>` use `rx="0.001"` to avoid Safari rounding bugs.

### When to use `inOut` vs `out`

- A path being "drawn" feels human-like with `inOut` — pen accelerates from rest, hits cruising speed, slows to a stop.
- A pure progress indicator feels more "data-driven" with `out`.

---

## 3. Scale overshoot bounce

Scene 1 social icons, Scene 3 logo, anywhere "pop in" is needed.

### Why `back.out(1.7)` and not three keyframes

`back.out(1.7)` is mathematically `back-easing with overshoot factor 1.7`. The element travels past 1.0 to ~1.07 and settles. Setting three keyframes (0% → 110% → 100%) at 0%, 70%, 100% timing produces nearly identical visuals but locks you out of GSAP's timeline coordination.

### Stagger pattern

```js
gsap.from(".social-icon", {
  scale: 0,
  opacity: 0,
  ease: "back.out(1.7)",
  duration: 0.5,
  stagger: 0.08,
});
```

`stagger: 0.08` = 80ms between each icon. For 5 icons that's 400ms total cascade — feels lively without dragging.

---

## 4. Mask pill wipe

Scene 2 reveal of "we change that".

### `clip-path` approach (preferred)

```html
<div class="reveal-text">we change that</div>
<style>
  .reveal-text {
    clip-path: inset(0 100% 0 0); /* hidden right side */
  }
</style>
```

```js
gsap.to(".reveal-text", {
  clipPath: "inset(0 0% 0 0)",
  duration: 0.6,
  ease: "power3.inOut",
});
```

### SVG `<mask>` approach (fallback)

If you need a non-rectangular mask shape, use SVG mask:

```html
<svg width="0" height="0">
  <defs>
    <mask id="pill-mask">
      <rect id="mask-pill" x="-200" y="0" width="200" height="80" rx="40" fill="white"/>
    </mask>
  </defs>
</svg>
<div style="mask:url(#pill-mask);">we change that</div>
```

Animate `#mask-pill`'s `x` attribute. Slower than `clip-path` but supports any shape.

### Sync the visible pill

The pink pill that appears to be doing the wiping is a SEPARATE element riding on top of the reveal. It needs its own position tween that matches the clip-path / mask edge. Synchronize via the same timeline so they can never desync.

---

## 5. Orbit rotation

Scene 3 icons rotating around the logo.

### Geometry

Place icons on a circle of radius `R` around a wrapper centered on the logo:

```js
const R = 220;
icons.forEach((icon, i) => {
  const angle = (i / icons.length) * Math.PI * 2;
  icon.style.left = `${Math.cos(angle) * R + 50}%`;
  icon.style.top = `${Math.sin(angle) * R + 50}%`;
});
```

### The rotation

```js
gsap.to(".orbit-wrapper", {
  rotation: 360,
  duration: 12,
  ease: "none", // EXCEPTION — orbits must be linear
  repeat: -1,   // EXCEPTION — orbits must loop
  transformOrigin: "50% 50%",
});
```

### Counter-rotate the icons (optional)

If you want icons to remain upright (not rotate with the orbit), counter-rotate each:

```js
gsap.to(".orbit-icon", {
  rotation: -360,
  duration: 12,
  ease: "none",
  repeat: -1,
});
```

---

## 6. Match-cut zoom

Scene 3 → Scene 4 transition. Logo scales until pink fills the screen, then Scene 4 (white) starts.

### Timing

```
t=3.6s: logo scale 1.0   (resting at end of Scene 3)
t=3.8s: logo scale 8     (filling about half the frame)
t=4.0s: logo scale 30    (pink covers everything)
t=4.0s: Scene 4 begins   (white background, logo invisible)
```

The trick: at scale 30, the logo's color becomes the background of Scene 4 for one frame. Then Scene 4 takes over with its own white background and the logo can disappear. Audience perceives a seamless wipe.

### Recipe

```js
tl.to("#scene3 .logo", {
  scale: 30,
  duration: 0.6,
  ease: "power3.inOut",
}, 3.4);
tl.set("#scene3", { display: "none" }, 4.0);
tl.set("#scene4", { display: "block" }, 4.0);
```

---

## 7. Ease-out slide

Scene 4 UI panels.

```js
gsap.from(".ui-panel", {
  x: -200,
  opacity: 0,
  duration: 0.7,
  ease: "power2.out",
  stagger: 0.1,
});
```

The 200px offset matches the panel sliding in from off-screen-left. For top-down: replace `x` with `y: -200`.

---

## 8. Anchor-point scaling

Chat bubbles "growing out of" an avatar.

```css
.chat-bubble {
  transform-origin: bottom left; /* or wherever avatar mouth is */
}
```

```js
gsap.from(".chat-bubble", {
  scale: 0,
  duration: 0.4,
  ease: "back.out(1.4)",
  stagger: 0.3, // 300ms between bubbles for natural conversation pacing
});
```

The `transform-origin` is the secret. Default `center` makes bubbles look like they're popping into existence; corner origins make them look like they're emerging from a source.

---

## 9. Pulsing loop

Scene 5 chip glow rings.

```js
gsap.to(".pulse-ring", {
  scale: 1.4,
  opacity: 0,
  duration: 1.6,
  ease: "power1.out",
  repeat: -1, // EXCEPTION
});
```

For multiple rings phased apart:

```js
gsap.to(".pulse-ring", {
  scale: 1.4,
  opacity: 0,
  duration: 1.6,
  ease: "power1.out",
  repeat: -1,
  stagger: { each: 0.4, repeat: -1 },
});
```

### Render-time consideration

`repeat: -1` is forbidden by hyperframes' renderer for top-level timelines because it has no end state. **It is only safe inside scenes with a fixed `data-duration`** — the scene's clip clips the loop's visibility. Don't put `repeat: -1` on your master timeline.

---

## 10. 2.5D rotation (radar rings)

Scene 5 angled rings dropping.

```html
<div class="radar" style="perspective: 800px;">
  <div class="ring" style="transform: rotateX(70deg);"></div>
</div>
```

```js
gsap.fromTo(".ring",
  { y: -100, opacity: 0 },
  { y: 200, opacity: 1, duration: 1.2, ease: "power1.in", stagger: 0.3 }
);
```

The `perspective` on the parent and `rotateX(70deg)` on the rings creates the "tilted into the screen" look. `power1.in` gives a subtle gravity feel.

---

## 11. Number counter

Scene 5 percentage counting down.

```js
const obj = { val: 46 };
gsap.to(obj, {
  val: 0,
  duration: 2,
  ease: "power2.inOut",
  onUpdate: () => {
    document.querySelector("#counter").textContent = Math.round(obj.val) + "%";
  },
});
```

### Why an object and not the DOM directly

GSAP can only tween numeric properties. `textContent` is a string, not a number. Tweening a stand-in object lets GSAP do the math, while `onUpdate` writes the formatted result.

### For currency, decimals, etc.

```js
onUpdate: () => {
  el.textContent = "$" + obj.val.toFixed(2);
}
```

---

## 12. Wiggle / shake

Scene 6 "Access denied" button.

```js
gsap.to("#deny-btn", {
  x: "+=8",
  duration: 0.05,
  repeat: 9,    // 10 total movements (5 cycles)
  yoyo: true,   // bounces back and forth
  ease: "none", // EXCEPTION — yoyo with ease feels mushy
});
```

Total duration: 0.05 × 10 = 0.5s. Distance: ±8px.

### Tuning

- More violent: increase distance to ±16px, decrease duration to 0.03s.
- Vertical shake (head-shaking "no"): change `x` to `y`.
- "Real" wiggle (per-frame randomness): forbidden — breaks deterministic rendering. Use the yoyo pattern.
