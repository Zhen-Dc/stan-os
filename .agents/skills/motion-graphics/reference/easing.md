# Easing Reference

The single most important decision in this skill. The wrong ease makes a $5,000 motion graphic look like a free PowerPoint transition.

## How to pick

Ask two questions:

1. **What kind of motion is this?**
   - Element appearing → use an **out** ease (decelerates as it arrives)
   - Element leaving → use an **in** ease (accelerates as it leaves)
   - Element moving from one resting state to another → use an **inOut** ease
2. **How "strong" should the deceleration feel?**
   - Subtle (UI nudge) → `power1`
   - Default (most everything) → `power2`
   - Dramatic (big reveal) → `power3` or `power4`
   - Bouncy (playful, attention-grabbing) → `back.out(N)` or `elastic.out`

## Curve picker

| Ease | Shape | When to use |
|---|---|---|
| `power1.out` | gentle decel | small UI nudges, opacity fades |
| `power2.out` | default decel | **the default for entrances** — slides, fades, scale-ins |
| `power3.out` | sharp decel | dramatic reveals, hero-element entrances |
| `power4.out` | very sharp decel | rare; only for "slamming into place" feel |
| `power2.inOut` | accelerate then decelerate | trim-path drawing, anything moving between two visible positions |
| `power3.inOut` | sharper inOut | scene-to-scene match-cut transitions |
| `back.out(1.7)` | overshoots past 100% then settles | bounce reveals (icons, pills, badges) |
| `back.out(1.4)` | gentler overshoot | chat bubbles, smaller UI elements |
| `elastic.out(1, 0.3)` | wobbles past target then settles | playful reveals — use sparingly, very attention-heavy |
| `expo.in` | almost-flat then sudden | exits in the final scene only |
| `power1.in` | gentle acceleration | radar rings dropping (gravity feel) |
| `none` (linear) | constant speed | **only** for orbit rotation (#5) and wiggle yoyo (#12) |

## ASCII curves (for intuition)

```
power2.out                back.out(1.7)
│      ╭──────             │      ╭───╮  ╭──
│    ╱                     │    ╱      ╰╱
│  ╱                       │  ╱
│╱                         │╱
└─────────                  └────────────

power2.inOut              expo.in
│         ╱                │            ╱
│       ╱                  │           ╱
│      ╱                   │         ╱
│    ╱                     │      ╱
│  ╱                       │ ───╯
└─────────                  └────────────
```

## GSAP syntax

```js
gsap.from(el, { x: -100, opacity: 0, ease: "power2.out", duration: 0.7 });
gsap.to(el,   { scale: 1.4, opacity: 0, ease: "power1.out", duration: 1.6, repeat: -1 });
```

The string-name form (`"power2.out"`) is preferred over the function form (`Power2.easeOut`) because it survives minification and doesn't require importing the ease.

## Anti-patterns

- `ease: "none"` outside the two whitelisted exceptions — fails the linter check.
- Mixing `back.out(1.7)` with `back.out(2.5)` in the same scene — one bounce intensity per scene unless you have a reason.
- `elastic.out` for serious / corporate / clean styles — it reads as "kid's cartoon."
- Using an `in` ease on an entrance — element accelerates as it arrives, which feels wrong (you want it to "land").

## Defer to GSAP skill

The hyperframes `gsap` sub-skill at `~/.claude/skills/hyperframes/skills/gsap/SKILL.md` has the full ease table, custom-cubic-bezier syntax, and `CustomEase` plugin details. Don't re-derive that here.
