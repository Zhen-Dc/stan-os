# Image QA

Generated at: 2026-07-02T22:02:43.6196231Z
Renderer: source/render_social_images.py
Version: v2
Previous version preserved at: versions/v1
PNG count: 20
GIF count: 1

## Generated Sets
- LinkedIn: linkedin-animation.gif primary, linkedin-thumbnail.png, linkedin-diagram.png fallback/poster
- Instagram: instagram-slide-01.png through instagram-slide-08.png
- X: x-thumbnail.png, x-quote-01.png through x-quote-06.png, x-quote.png
- Facebook: facebook-thumbnail.png, facebook-course-card.png

## Manual Inspection
Inspected representative outputs:
- drafts/Instagram/images/instagram-slide-01.png
- drafts/Instagram/images/instagram-slide-02.png
- drafts/Instagram/images/instagram-slide-03.png
- drafts/Instagram/images/instagram-slide-04.png
- drafts/Instagram/images/instagram-slide-05.png
- drafts/Instagram/images/instagram-slide-06.png
- drafts/Instagram/images/instagram-slide-07.png
- drafts/Instagram/images/instagram-slide-08.png
- drafts/LinkedIn/images/linkedin-thumbnail.png
- drafts/LinkedIn/images/linkedin-diagram.png
- drafts/LinkedIn/images/linkedin-animation.gif file exists and contains 5 highlighted-step frames

## Checks Passed
- Slide 1 uses the clean intro cover with the approved title.
- Slides 2-6 map to source use cases 1-5 in order.
- Slide 5 correctly represents use case 4: code review.
- Slide 6 correctly represents use case 5: PRD-backed custom software.
- Slides 7-8 are filter/recap slides, not mislabeled source use cases.
- Prompt boxes are labeled `PROMPT`.
- Instruction panel is labeled `INSTRUCTION`.
- Checklist and QA panels are labeled `CHECKLIST` or `QA GATE`.
- LinkedIn visual uses the approved "strongest AI model" title.
- Stanley's real avatar appears in inspected creator rows.
- No obvious clipping, overlap, or unreadable text was found in inspected images.

## Known Issues
The visuals are deterministic local rendered drafts, not GPT-generated raster art. They are intentionally text-forward and editable by rerunning the package renderer.
