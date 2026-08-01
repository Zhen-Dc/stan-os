# Visual Recipes

Use these recipes when generating prompts for `gpt-image-2`.

## Shared Prompt Rules

- Use platform-specific aspect ratios.
- Always create a first intro/thumbnail image before supporting visuals. This cover should tell viewers what they are about to see before the carousel, slider, quote set, or post details begin.
- Match the reference structure: subtle cream or off-white paper/grid background, compact top badge/pill, oversized editorial headline, one rust/orange accent word or number, short supporting subhead, creator row, and small slide count or swipe cue when relevant. Use spacious composition for intro covers and dense, information-rich composition for teaching slides.
- For roundup/list posts, use the alternate reference pattern: large central title with numbered mini-cards around it, curved arrows showing sequence, compact read-time/value pills, and small source/creator footer.
- Keep text short and readable.
- Prefer one key sentence on the image.
- The visible text must be a lesson, fact, framework step, or useful takeaway from the video source. Use the transcript/script when available; if blocked, use only verified metadata, description, chapters, and the written source brief.
- Do not invent direct quotes, unrelated AI advice, or generic motivational text.
- Include enough visual structure to communicate process, proof, or insight.
- Avoid fake logos, fake screenshots, private client data, and unverifiable numbers.
- If using anonymized proof, describe it as blurred or redacted.
- Use Stanley's brand avatar from `AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png` when a creator avatar appears.
- Measure or visually reserve enough room for the creator name before placing the verified badge; the badge must sit to the side of the name, not on top of it.
- Inspect every final PNG before handoff. Reject generated lookalike avatars and any image where Stanley's real profile picture is pasted over another visible face.

## Intro Thumbnail / Carousel Cover

Use this recipe for the first image in every visual set.

The intro/cover must always be clean and structured like Stanley's reference cover: spacious cream grid background, one dark badge, one oversized headline, one accent word or line, one short subhead, creator row near the lower-left, and a simple swipe/count cue. Do not use the detailed teaching-slide layout for the intro.

When the user wants the former/local image technique or says not to use GPT image generation, render these with `scripts/render_reference_style_images.py` instead of an image model. The renderer should preserve the same reference pattern: cream graph-paper background, top creator pill, numbered title pill, cards, prompt boxes, footer count, and swipe cue.

For carousel intro images, keep the cover focused only on the main subject. Do not include step cards, prompt/action boxes, diagrams, or the teaching sequence on the intro. The intro should feel like the reference cover: one punchy scroll-stopping title, one short catchy subtext, a small badge/pill, creator row, slide count, and swipe cue. The teaching starts on the next slide numbered `1`.

Aspect ratios:

- Instagram carousel: 1080x1350.
- LinkedIn: 1200x1200 or 1200x627.
- X: 920x458 white tweet screenshot image, content-tight with no extra top or bottom margin.
- Facebook: 1080x1350 or 1200x1500.

Prompt pattern:

```text
Create the intro/thumbnail image for a social post or carousel about "[TOPIC]".

Headline: "[BIG SIMPLE SCROLL-STOPPING TITLE THAT MATCHES THE BLOG TOPIC]"
Badge text: "[SHORT CONTEXT BADGE, e.g. AI WORKFLOW, BUILT WITH AI, PROMPT SYSTEM]"
Subhead: "[SHORT CATCHY DESCRIPTION, CLOSE TO THE BLOG INTRO, THAT MAKES THE VIEWER WANT TO OPEN THE POST]"
Creator row: "Stanley • @stanleyai" with Stanley's brand avatar from AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png when available.
Footer cue: "[01 / TOTAL]" on the left and "SWIPE" with a small arrow on the right when this is a carousel/slider.

Visual style: cream/off-white graph-paper background, editorial poster layout, oversized dark navy/black headline, one rust/orange accent word or number, compact rounded badge near the top, creator pill near the lower-left, minimal icon or mascot if relevant, lots of whitespace, crisp readable typography.

Do not include steps, prompt boxes, action boxes, or detailed diagrams on the cover. Do not copy the reference image exactly. Recreate the structure and pattern for Stanley's brand. Keep all text legible and avoid distorted letters.
```

Alternate roundup pattern:

```text
Create an infographic-style intro thumbnail for a roundup post about "[TOPIC]".

Center title: "[NUMBER] [ITEMS/LESSONS/TOOLS] to [OUTCOME]"
Surrounding cards: [NUMBER] small rounded cards arranged around the center, each with a number, short title, small time/value pill, and one short description.
Flow: curved arrows connecting the cards in sequence.
Footer: small source/creator note.

Visual style: off-white background, black editorial serif/sans mix, rust/orange numbered circles and pills, soft card shadows, spacious layout, readable at phone size.
```

## LinkedIn Key-Takeaway Graphic

Aspect ratio: 1200x1200 or 1200x627.

First create `thumbnail-prompt.txt` using the Intro Thumbnail / Carousel Cover recipe. Then create the supporting LinkedIn animated GIF prompt below. For this workflow, the primary LinkedIn visual should be an animated GIF when the post explains a process, framework, or sequence. Keep a static PNG poster only as a fallback.

Prompt pattern:

```text
Create a LinkedIn educational animated GIF for an AI automation services brand.
Main title: "[VIDEO TITLE OR CLEAR FRAMEWORK TITLE]"
Structure: 3-5 numbered steps, each with concise annotations, small interface sketches, arrows, and description blocks. Animate by highlighting one step per frame.
Visual style: polished whiteboard or hand-drawn diagram, dense but readable, black text, blue and green accents, professional educational feel.
Include Stanley's profile photo as a small creator avatar when available and add a small blue verified badge next to the name.
Output format: GIF, with an optional PNG poster fallback.
Do not include fake company logos. Keep text legible and avoid distorted words.
```

## X Quote Graphic

Canvas: 920x458, matching the accepted content-tight X tweet aspect ratio.

First create `thumbnail-prompt.txt` using the Intro Thumbnail / Carousel Cover recipe. Then create the quote-card set below.

Create six different X tweet images by default:

- `x-quote-01.png`
- `x-quote-02.png`
- `x-quote-03.png`
- `x-quote-04.png`
- `x-quote-05.png`
- `x-quote-06.png`

Also copy `x-quote-01.png` to `x-quote.png` for compatibility with older previews.

Prompt pattern:

```text
Create a clean tweet screenshot-style slide for X about the lesson from this source.
Tweet text: "[SHORT SOURCE-DERIVED LESSON OR FACT]"
Visual style: plain white 920x458 canvas like a tweet screenshot. Place Stanley's avatar, the bold name "Stanley", a small blue verified badge immediately after the name, and the gray @stanleyai handle on one horizontal creator row near the top-left. Put large black tweet text underneath with paragraph spacing. Keep the image tight to the tweet content with no extra top or bottom margin.
Output format: PNG.
No slide-count pill, no border, no cream grid, no action row, no timestamp, no prompt box, no fake engagement numbers, no decorative carousel frame, and no clutter.
```

## Instagram Structured Tweet-Style Carousel

Aspect ratio: 1080x1350 per slide.

Slide 1 must always be the intro/thumbnail cover using the Intro Thumbnail / Carousel Cover recipe. Supporting slides start after the cover and should teach the framework, steps, or key ideas.

After the intro/thumbnail cover, restart the instructional numbering at 1. For example, an 8-slide carousel should have slide 1 as the cover, then the first teaching slide should display `1`, not `2`.

Supporting slides must always use the structured reference layout, not a sparse quote-card layout: top-right creator pill, numbered circle, colored title pill, body hook, diagram/cards/comparison block, "APPLY THIS" or "SAVE THIS" action box, and bottom swipe/count cue.

Supporting slides should be information-rich and varied. Do not default every lower section to a prompt box. Choose the module that fits the slide's actual lesson:

- `PROMPT` or `PASTE THIS` when the viewer should copy an instruction.
- `INSTRUCTION` when the viewer should follow a rule but does not need a copyable prompt.
- `TECH STACK` when the lesson is about tools, surfaces, models, connectors, or outputs.
- `TIPS` when the lesson is a set of tactical rules.
- `CHECKLIST` or `QA GATE` when the lesson is quality control, review, or acceptance criteria.
- `WORKFLOW` when the lesson is a process with stages, handoffs, or outputs.
- `ROUTINE` when the lesson is schedule-based or runs repeatedly.
- `ROLES`, `TOOLS`, or `OUTPUT` when the slide is explaining an operating system, team, or pipeline.
- `SAVE THIS` or `USE THIS` when the slide is a recap or decision filter.

Use the available canvas. Reference-style teaching slides should feel full of useful information: title, explanation, visual block, module panel, footer cue, and supporting chips/rows where relevant. Dense does not mean cramped; keep readable spacing, but avoid large unused blank zones unless the slide is the intro cover.

The module label must match the content. If the box contains a prompt, state `PROMPT`. If it contains tips, state `TIPS`. If it contains an instruction, state `INSTRUCTION`. If it is a review gate, state `QA GATE`. Do not make viewers infer what the lower panel is.

Do not place the same `BOTTOM LINE` panel on most supporting slides. Use varied
closing modules, different panel placements, or no closing panel when the main
body already carries the lesson. Repetition should not make different slides
look like the same template.

Before rendering, compare the carousel to the main post. Each slide must follow the same source-derived sequence, use the correct numbering, and be understandable without jargon. If slide 4 is supposed to be use case 4, it cannot talk about use case 5.

Each supporting carousel slide should follow the reference detail pattern:

- Top-right creator pill with the real profile photo and handle.
- Numbered circle plus colored rounded title pill.
- One clear explanatory paragraph under the heading.
- A structured visual block such as rows, cards, command boxes, tool chain, schedule rows, comparison cards, checklist, or a simple workflow diagram.
- A lower module panel with a label that matches the content: prompt, instruction, tech stack, tips, checklist, workflow, routine, roles, tools, output, QA gate, save this, or use this.
- Bottom-left slide count and bottom-right swipe cue.
- Clean cream graph-paper background, strong dark headline type, one accent color per slide, and generous spacing.

Do not make sparse quote-only carousel slides when the reference asks for a detailed carousel. Use quote cards only for X-specific quote graphics.

Prompt pattern:

```text
Create slide [N] of an educational Instagram carousel with a clean structured tweet-style layout.
Slide title: "[NUMBERED STEP TITLE]"
Body text: "[ONE SHORT TEACHING POINT]"
Visual block: "[SIMPLE ROWS, CODE WINDOW, TOOL STACK, COMPARISON CARDS, CHECKLIST, OR 3-STEP FLOW]"
Lower module: "[PROMPT, INSTRUCTION, TECH STACK, TIPS, CHECKLIST, WORKFLOW, ROUTINE, ROLES, TOOLS, OUTPUT, QA GATE, SAVE THIS, OR USE THIS]"
Visual style: warm cream grid background, top-right creator pill, Stanley's circular profile photo, @stanleyai handle, small blue verified badge placed beside the creator name with clear spacing, rounded colored title pill, simple diagram/card section, paste/action card near the bottom, and small swipe footer.
Output format: PNG.
Keep the slide text-first, dense, and readable. Use most of the canvas with useful source-derived information, not decorative whitespace. No fake platform buttons. No tiny text. Avoid placing text blocks so close that labels overlap containers.
```

## Facebook Course-Interest Graphic

Aspect ratio: 1200x1500 or 1080x1350.

First create `thumbnail-prompt.txt` using the Intro Thumbnail / Carousel Cover recipe. Then create the supporting course-interest graphic prompt below if the post needs an additional visual.

Prompt pattern:

```text
Create a beginner-friendly Facebook course-interest graphic for people learning AI skills.
Main text: "[LEARNING OUTCOME]"
Visual style: warm but professional, simple AI workflow illustration, laptop/dashboard motif, confidence-building, readable text, generous padding inside every text block.
Avoid luxury imagery and unrealistic income promises.
Do not let text touch or clip against the bottom of containers or the canvas.
```

## QA Checklist

- Text is legible at phone size.
- The image makes sense without the caption.
- The claim is safe and supported.
- The visual matches the platform lane.
- The design is not overcrowded.
