# FemLink Arc Template

A 6-scene motion-graphic composition that recreates the FemLink-style explainer aesthetic. Renders to ~25 seconds of polished animation via hyperframes.

## Six scenes

| # | Scene | Time | Story beat |
|---|---|---|---|
| 1 | Problem | 0:00–0:02 | Pain stat with radial dial |
| 2 | Transition | 0:03–0:05 | "Today we change that" |
| 3 | Reveal | 0:05–0:09 | Logo + orbiting icons → match-cut zoom |
| 4 | Interface | 0:09–0:14 | UI mock with sliding panels |
| 5 | Tech | 0:14–0:19 | Chip + radar + counter |
| 6 | Outro | 0:19–0:25 | Lockout / CTA → fade to logo |

## Use in 4 steps

### 1. Collect inputs (the skill does this)

The motion-graphics skill MUST ask the user for these before populating the template:

- Primary color (hex)
- Accent color (hex)
- Background tone — `light` / `dark` / `flat`
- Brand name (text shown in Reveal)
- Tagline (text shown in Transition, e.g. "we change that")
- Optional: logo file path
- Optional: target duration (default 25s)

### 2. Copy the template into the project

```
edit/
├── composition.html   ← copy from templates/femlink-arc/composition.html
└── palette.css        ← copy from templates/femlink-arc/palette.css
```

### 3. Substitute placeholders

In `palette.css`:

- `{{PRIMARY_HEX}}` → user's primary
- `{{ACCENT_HEX}}` → user's accent
- `{{BRAND_NAME}}` → user's brand
- `{{TAGLINE}}` → user's tagline
- Uncomment ONE of the three tone blocks (LIGHT / DARK / FLAT)

In `composition.html`:

- `{{LOGO_SRC}}` → path to logo file, or remove the `<img>` tag if user has no logo
- `{{STAT_HEADLINE}}` → the "FOR YEARS" line
- `{{STAT_VALUE}}` → the percentage shown by the dial (e.g. `80`)
- `{{STAT_CAPTION}}` → small print under the dial
- `{{TECH_PERCENTAGE}}` → starting value for Scene 5 counter (default `46`)

### 4. Preview, lint, render

```bash
cd ~/.claude/skills/hyperframes
npx hyperframes preview                                   # open in browser
npx hyperframes lint --composition <path>                 # validate
npx hyperframes render --composition <path> --output edit/final_with_graphics.mp4
```

## Customization

- **Re-skin only:** change `palette.css` values. The template will follow.
- **Re-time:** edit `data-start` and `data-duration` on each scene's root `<section>`. Update the GSAP timeline scene anchors at the bottom of the file accordingly.
- **Add a scene:** insert a new `<section>` between Scenes 4 and 5; assign `data-start="14"` and shift Scenes 5 and 6 forward. Update the timeline.

## Hard rules — DO NOT VIOLATE

1. Never write a hex color into `composition.html`. Use `var(--primary)` etc.
2. Never default the palette. Always ask the user.
3. The orbit rotation (Scene 3) and pulsing loop (Scene 5) are the ONLY `repeat: -1` tweens. Adding one elsewhere breaks rendering.
4. Final scene is the only scene with exit animations.
