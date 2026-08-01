---
name: motion-graphics
description: Add motion graphics to videos using the FemLink-style 6-scene arc (Problem → Transition → Reveal → Interface → Tech → Outro) and a technique library covering easing, radial wipes, trim paths, scale-overshoot bounces, mask wipes, orbit rotation, match-cut zooms, pulsing loops, 2.5D radar tilts, animated number counters, wiggle/shake, and neumorphic styling. Use this skill when the user asks to add motion graphics, animated lower thirds, animated UI, animated text, or polish/intro/outro to a video — especially after a video-use edit pass. Outputs HTML compositions that the hyperframes skill renders to MP4. ALWAYS asks for color palette, brand name, and typography before generating.
---

# Motion Graphics

This skill turns the design philosophy of a polished motion-graphic explainer (the "FemLink" video — see `reference/case-study-femlink.md`) into a reusable system. Every video this skill produces is built from two ingredients:

1. **A scene-arc template** — the 6-scene narrative formula (Problem → Transition → Reveal → Interface → Tech → Outro) lives in `templates/femlink-arc/composition.html`. Colors, typography, and brand are CSS variables, never hardcoded.
2. **A technique library** — 12 named techniques (radial wipe, trim path, scale-overshoot, mask wipe, orbit rotation, match-cut zoom, ease-out slide, anchor-point scaling, pulsing loop, 2.5D rotation, number counter, wiggle/shake) — each with a worked HTML example in `examples/`.

## Pipeline integration

```
raw video ──[video-use skill]──> edit/final.mp4 ──[motion-graphics skill]──> edit/composition.html ──[hyperframes skill]──> edit/final_with_graphics.mp4
```

This skill produces the HTML composition. It does NOT render. Rendering is delegated to hyperframes:

```bash
cd ~/.Codex/skills/hyperframes
npx hyperframes preview                              # iterate visually first
npx hyperframes lint --composition <path>            # validate before render
npx hyperframes render --composition <path> --output edit/final_with_graphics.mp4
```

## Core principle: easing first

Nothing in this style moves at constant speed. Every animation accelerates and decelerates. If you are tempted to write `ease: "none"` or `ease: "linear"`, stop — there is almost certainly a better choice.

The four default eases:

| Use case | Ease |
|---|---|
| Element entrance (slide / fade in) | `power2.out` |
| Scene-to-scene transition | `power3.inOut` |
| Bounce / overshoot reveal (icons, buttons) | `back.out(1.7)` |
| Element exit (final scene only) | `expo.in` |

Deeper easing reference: `reference/easing.md`. GSAP easing math itself lives in the hyperframes `gsap` sub-skill — defer there for transform aliases and callback details.

## Setup protocol — ASK BEFORE GENERATING

**Hard rule:** before producing any composition, ask the user for the values below in a single round of questions. Do NOT default to FemLink pink or any other palette. Do NOT begin writing the HTML until you have answers.

Required:

1. **Primary color** — main brand hue (hex)
2. **Accent color** — secondary highlight (hex)
3. **Background tone** — `light` (warm off-white #F0EAE2-style neumorphic) / `dark` (deep neutral neumorphic) / `flat` (no neumorphic shadows)
4. **Brand name** — text shown in the Reveal scene
5. **Tagline** — short phrase for the Transition scene (e.g., "we change that")

Optional:

6. **Logo source** — path or URL; if omitted, the brand name renders as a typographic logo
7. **Target duration** — defaults to 25 seconds matching the case study; can stretch/compress per scene

Once collected, write these into `edit/palette.css` (copy from `templates/femlink-arc/palette.css`) and reference via CSS variables in the composition.

## Technique catalog

Each technique below maps a visual goal to a GSAP recipe and the matching standalone example. Copy the example, swap palette variables, drop into the scene where it belongs.

### 1. Radial wipe (Scene 1 — pink dial)

**Goal:** circular progress bar fills from 0 to N% with eased deceleration.
**Recipe:** SVG `<circle>` with `stroke-dasharray` equal to circumference; animate `stroke-dashoffset` from full to `(1 - percent) × circumference`. Ease `power2.out`.
**Example:** `examples/radial-wipe.html`

### 2. Trim path (Scene 1 — graph line)

**Goal:** line is "drawn" from left to right.
**Recipe:** SVG `<path>` with `stroke-dasharray: pathLength` and `stroke-dashoffset: pathLength`; tween offset to 0. Ease `power2.inOut`.
**Example:** `examples/trim-path.html`

### 3. Scale overshoot bounce (Scene 1 — social icons)

**Goal:** elements pop in past 100% then settle.
**Recipe:** `gsap.from(el, { scale: 0, ease: "back.out(1.7)", duration: 0.5, stagger: 0.08 })`. The `back.out(1.7)` ease bakes in the 0% → 110% → 100% overshoot; do NOT chain three keyframes manually.
**Example:** `examples/scale-bounce.html`

### 4. Mask pill wipe (Scene 2 — "we change that" reveal)

**Goal:** a moving shape acts as a mask that reveals underlying text.
**Recipe:** put text inside a container with `clip-path: inset(0 100% 0 0)`; tween `clip-path` to `inset(0 0% 0 0)`. The pill shape rides on top with its own position tween, syncing the visual edge.
**Example:** `examples/mask-pill-wipe.html`

### 5. Orbit rotation (Scene 3 — icons around logo)

**Goal:** ring of icons rotates continuously around an anchor.
**Recipe:** wrapper div centered on the logo; absolutely-positioned icons placed on a circle inside it; `gsap.to(wrapper, { rotation: 360, duration: 12, ease: "none", repeat: -1 })`. **Linear is the exception here** — orbital rotation must be constant-velocity to look mechanical, not springy.
**Example:** `examples/orbit-rotation.html`

### 6. Match-cut zoom (Scene 3 → Scene 4 transition)

**Goal:** logo or shape scales until it fills the frame, becoming the next scene's background.
**Recipe:** scale element from 1 to ~40 with `ease: "power3.inOut"` over ~0.6s. The element's color becomes the next scene's background. Time the scene boundary so the new scene starts the moment scale crosses ~30.
**Example:** `examples/match-cut-zoom.html`

### 7. Ease-out slide (Scene 4 — UI elements)

**Goal:** UI panels slide in fast and decelerate to rest.
**Recipe:** `gsap.from(el, { x: -200, opacity: 0, ease: "power2.out", duration: 0.7 })`. Stagger by 0.1s for sequential reveal.
**Example:** `examples/ease-out-slide.html`

### 8. Anchor-point scaling (Scene 4 — chat bubbles)

**Goal:** chat bubbles "grow out of" the avatar's mouth.
**Recipe:** set `transform-origin: bottom left` (or matching corner); animate `scale: 0 → 1` with `ease: "back.out(1.4)"`.
**Example:** included in `examples/ease-out-slide.html` (chat-bubble subsection)

### 9. Pulsing loop (Scene 5 — chip glow)

**Goal:** glowing rings expand and fade continuously.
**Recipe:** `gsap.to(ring, { scale: 1.4, opacity: 0, duration: 1.6, ease: "power1.out", repeat: -1 })`. **The only place in the skill where `repeat: -1` is permitted** outside of orbit rotation.
**Example:** `examples/pulsing-loop.html`

### 10. 2.5D rotation (Scene 5 — radar rings)

**Goal:** flat 2D rings tilted into 3D space, falling downward.
**Recipe:** wrapper with `perspective: 800px`; rings have `transform: rotateX(70deg)`; tween `y` from 0 to 200 with `ease: "power1.in"`, staggered.
**Example:** `examples/radar-2_5d.html`

### 11. Number counter (Scene 5 — percentage drop)

**Goal:** integer counts smoothly between two values.
**Recipe:** create an object `{ val: 46 }`, tween it with `gsap.to(obj, { val: 0, ease: "power2.inOut", duration: 2, onUpdate: () => el.textContent = Math.round(obj.val) + "%" })`.
**Example:** `examples/number-counter.html`

### 12. Wiggle / shake (Scene 6 — "Access denied")

**Goal:** rapid horizontal wobble communicating error.
**Recipe:** `gsap.to(el, { x: "+=8", duration: 0.05, repeat: 9, yoyo: true, ease: "none" })`. Total ~0.5s. Do not use random — every frame is deterministic.
**Example:** `examples/wiggle-shake.html`

## Scene archetypes — the FemLink arc

The 6 scenes in `templates/femlink-arc/composition.html` follow this narrative formula. Treat them as a story spine, not just timing slots.

| # | Scene | Time | Story beat | Techniques used |
|---|---|---|---|---|
| 1 | Problem | 0:00–0:02 | "FOR YEARS" — show a stat or pain point | Radial wipe, trim path, scale-overshoot |
| 2 | Transition | 0:03–0:05 | "Today we change that" | Mask pill wipe |
| 3 | Reveal | 0:05–0:09 | "Introducing {brand}" — logo with orbiting icons → match-cut zoom | Orbit rotation, match-cut zoom |
| 4 | Interface | 0:09–0:14 | UI mock — search bar, chat, video player | Ease-out slide, anchor-point scaling |
| 5 | Tech | 0:14–0:19 | Engine / under-the-hood — chip + radar + counter | Pulsing loop, 2.5D rotation, number counter |
| 6 | Outro | 0:19–0:25 | Lockout fail OR call-to-action; fade to logo | Wiggle/shake, fade |

Per-scene wiring lives in `templates/femlink-arc/composition.html`. To re-skin: change palette only. To extend: add a new scene as Scene 4.5 with `data-start` after Scene 4's end.

## Neumorphic design rules

Neumorphic surfaces simulate a single soft light source from the **upper left**. Each panel needs one highlight (top-left) and one soft shadow (bottom-right):

```css
/* Light tone */
.panel {
  background: var(--bg-tone);
  border-radius: 24px;
  box-shadow:
    -8px -8px 16px rgba(255, 255, 255, 0.7),
     8px  8px 16px rgba(0, 0, 0, 0.12);
}

/* Dark tone */
.panel-dark {
  background: var(--bg-tone);
  box-shadow:
    -6px -6px 14px rgba(255, 255, 255, 0.05),
     6px  6px 14px rgba(0, 0, 0, 0.55);
}
```

Pressed/inset elements (input fields, dial troughs) invert the shadow direction — use `inset` keyword. Full reference: `reference/neumorphic.md`.

## Hard rules — non-negotiable

1. **Always ask for the palette before writing any HTML.** Defaults are forbidden.
2. **Every animation must have an ease.** `ease: "none"` is permitted only inside orbit rotation (#5) and the wiggle yoyo (#12).
3. **No `Math.random()`.** Every frame must be deterministic so renders are reproducible.
4. **`repeat: -1` is permitted only in orbit rotation (#5) and pulsing loop (#9).** Anywhere else it breaks render finalization.
5. **All clips must have `data-start`, `data-duration`, and `data-track-index`** — these are hyperframes contract requirements.
6. **All colors come from CSS variables.** Never write a hex literal in `composition.html` — only in `palette.css`.
7. **Final scene is the only scene with exit animations.** Earlier scenes end by transitioning to the next, not by fading out.
8. **Subtitles from video-use must survive.** When the source video has burned subtitles, place the video element in the composition with subtitles already burned-in — do not re-render subtitles on top.

## Anti-patterns

- **Linear motion.** Almost always wrong. Audit your tweens — if you see `ease: "none"` outside the two exceptions, change it.
- **Hardcoded brand colors.** If you typed `#FF` into composition.html, you bypassed the palette protocol. Fix.
- **Re-implementing GSAP eases by hand.** Defer to GSAP's named eases. The hyperframes `gsap` sub-skill has the full list.
- **Skipping the palette prompt** because the user said "just use defaults." Ask anyway — give them sensible options to pick from.
- **Adding a 7th scene without re-balancing timing.** The arc is calibrated; if you must add, also adjust durations so the total still feels paced.

## Files in this skill

- `SKILL.md` — this file
- `reference/case-study-femlink.md` — original scene-by-scene breakdown (the source case study)
- `reference/easing.md` — easing taxonomy and curve picker
- `reference/techniques.md` — long-form technique reference
- `reference/neumorphic.md` — soft-shadow design rules
- `templates/femlink-arc/composition.html` — 6-scene template
- `templates/femlink-arc/palette.css` — CSS variables, populated at use time
- `templates/femlink-arc/README.md` — template usage guide
- `examples/*.html` — 11 standalone technique demos
