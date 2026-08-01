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
- `drafts/Instagram/images/instagram-slide-04.png`
- `drafts/Instagram/images/instagram-slide-06.png`
- `drafts/LinkedIn/images/linkedin-diagram.png`
- `drafts/X/images/x-quote-03.png`
- `drafts/Facebook/images/facebook-course-card.png`

## Instagram carousel QA

- Slide 1 uses the clean cover layout.
- Slides 2-8 use dense teaching layouts with structured cards and module panels.
- Module variety is present: WORKFLOW, CHECKLIST, TIPS, ROLES, QA GATE, AUTOMATION MAP, SAVE THIS.
- Lower module labels match the slide content.
- A bottom takeaway strip was added to teaching slides to avoid unused blank space.

## Text and layout QA

- Text is readable at phone size in inspected images.
- No clipping or overlap was visible in inspected images.
- The verified badge has spacing beside the creator name.
- X images use the clean tweet screenshot style with no fake engagement row.
- Facebook images avoid income promises and use beginner-friendly learning language.

## Known issues

- The GIF is generated locally from static highlighted frames rather than a model-generated animation. This matches the deterministic local-renderer workflow and keeps text readable.
