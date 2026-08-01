# Image QA

## Generated media

- PNG count: 20
- GIF count: 1
- LinkedIn GIF: `drafts/LinkedIn/images/linkedin-animation.gif`
- LinkedIn GIF frames: 5

## Avatar check

- Stanley's real avatar from `asset-folder/Brand_Assets/Stan Avatar.png` is used in the rendered visuals.
- No generated lookalike or fake stock avatar was used.

## Representative images inspected

- `drafts/Instagram/images/instagram-slide-01.png`
- `drafts/Instagram/images/instagram-slide-03.png`
- `drafts/Instagram/images/instagram-slide-05.png`
- `drafts/Instagram/images/instagram-slide-06.png`
- `drafts/Instagram/images/instagram-slide-08.png`
- `drafts/LinkedIn/images/linkedin-diagram.png`
- `drafts/X/images/x-quote-03.png`
- `drafts/Facebook/images/facebook-course-card.png`
- `preview/instagram-contact-sheet-v3.png`

## Instagram carousel QA

- Slide 1 keeps the clean intro but adds useful subtext and a WHAT TO SAVE chip row.
- Slides 2-8 no longer share the same prompt-box layout.
- Layout variety is present: WORKFLOW comparison, CHECKLIST grid, TIPS comparison, INSTRUCTION flow, TECH STACK folder board, AUTOMATION MAP table, and SAVE THIS decision filter.
- Prompt, tip, instruction, checklist, workflow, and tech-stack panels are labeled clearly when used.
- Each slide carries enough context to work as a standalone post instead of only a continuation of the previous slide.

## Text and layout QA

- Text is readable at phone size in inspected images.
- No clipping or overlap was visible in inspected images.
- The verified badge has spacing beside the creator name.
- LinkedIn image and GIF use the same standalone title: "Stop Retyping AI Instructions."
- X images use the clean tweet screenshot style with no fake engagement row, and each card reads as its own standalone post.
- Facebook images avoid income promises and use beginner-friendly learning language.
- The old repeated takeaway label was replaced with varied audience-facing labels such as WHY IT MATTERS, CHECK THIS, CUSTOM RULE, PROMPT NOTE, SYSTEM MAP, and SAVE THIS.

## Known issues

- The GIF is generated locally from static highlighted frames rather than a model-generated animation. This matches the deterministic local-renderer workflow and keeps text readable.
