# Neumorphic Design Reference

Neumorphism = soft UI surfaces that look pressed out of (or into) the background. The defining feature: **a single soft light source from the upper-left**. Every surface has one bright highlight (top-left) and one soft shadow (bottom-right).

## The single rule

```css
box-shadow:
  -<offset>px -<offset>px <blur>px <highlight-color>,
   <offset>px  <offset>px <blur>px <shadow-color>;
```

That's it. Two shadows, opposite directions, opposite colors.

## Light tone (default — warm off-white background)

```css
:root {
  --bg-tone: #F0EAE2;        /* warm off-white */
  --highlight: rgba(255, 255, 255, 0.7);
  --shadow: rgba(0, 0, 0, 0.12);
}

.panel {
  background: var(--bg-tone);
  border-radius: 24px;
  padding: 32px;
  box-shadow:
    -8px -8px 16px var(--highlight),
     8px  8px 16px var(--shadow);
}
```

## Dark tone

```css
:root {
  --bg-tone: #2A2A35;
  --highlight: rgba(255, 255, 255, 0.05);
  --shadow: rgba(0, 0, 0, 0.55);
}

.panel-dark {
  background: var(--bg-tone);
  border-radius: 24px;
  padding: 32px;
  box-shadow:
    -6px -6px 14px var(--highlight),
     6px  6px 14px var(--shadow);
}
```

Dark neumorphic uses smaller offsets (6 vs 8) and weaker highlights — too much white in dark mode looks like fingerprint smudges.

## Pressed (inset) variant

For input fields, dial troughs, sliders — anything that should look depressed into the surface:

```css
.input-pressed {
  background: var(--bg-tone);
  border-radius: 16px;
  box-shadow:
    inset  4px  4px 8px var(--shadow),
    inset -4px -4px 8px var(--highlight);
}
```

Notice the order is inverted: shadow on top-left (where the rim casts onto the well), highlight on bottom-right (where the well's far edge catches light).

## Sizing rules

| Surface size | Offset | Blur |
|---|---|---|
| Small (button, icon ~64px) | 4px | 8px |
| Medium (card ~300px) | 8px | 16px |
| Large (panel ~600px+) | 12px | 24px |

The shadow should be visible but not dominant. If your panel looks like it's floating high above the background, halve the offset.

## Border-radius matters

Neumorphic surfaces look wrong with sharp corners. Minimum `border-radius: 16px` for small elements, `24-32px` for panels. Pill shapes (`border-radius: 999px`) look great.

## Color rules

- The surface color must equal the background color. If the panel is darker than the background, the shadows lie about the geometry and the illusion breaks.
- Brand colors (primary/accent) appear on TOP of neumorphic surfaces — as text, icons, dial fills, accents — never as the surface color itself.
- Gradients on the surface are forbidden in strict neumorphism. They wreck the lighting model.

## Palette-aware shadow generation

When the user picks a `light` background tone, derive `--bg-tone`, `--highlight`, `--shadow` automatically:

```css
/* User picks: --primary: #E91E63; --accent: #FFC107; tone: light */
:root {
  --primary: #E91E63;
  --accent: #FFC107;
  --bg-tone: #F0EAE2;
  --highlight: rgba(255, 255, 255, 0.7);
  --shadow: rgba(0, 0, 0, 0.12);
}
```

For `dark`:
```css
:root {
  --primary: #E91E63;
  --accent: #FFC107;
  --bg-tone: #2A2A35;
  --highlight: rgba(255, 255, 255, 0.05);
  --shadow: rgba(0, 0, 0, 0.55);
}
```

For `flat` (no neumorphic):
```css
:root {
  --primary: #E91E63;
  --accent: #FFC107;
  --bg-tone: #FFFFFF;
  --highlight: transparent;
  --shadow: transparent;
}
.panel { box-shadow: none; }
```

## Anti-patterns

- Multi-directional shadows ("blur from all sides") — kills the light-source illusion.
- Shadow color = pure black — too harsh; always low-alpha.
- Highlight color = pure white — same; especially in dark mode.
- Background color ≠ surface color — the most common mistake. They MUST match.
- Heavy gradients inside the surface — flattens the depth.
