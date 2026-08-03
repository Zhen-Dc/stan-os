# SOP: Repurpose Social Full Package For Dumb Models

## Purpose

Use this SOP whenever the `repurpose-youtube-video` skill turns one source into
LinkedIn, Instagram, X, and Facebook content for Stanley. For any web URL, use
the v3 skill copy so Firecrawl captures the source before drafting.

This SOP exists so a weak model does not drift into generic layouts, sparse
slides, repeated prompt boxes, or text-only packages. Follow it literally.

The final output is a complete local package under:

```text
AIS-OS/asset-folder/content/<source-title-slug>/
```

The package is not complete until it has:

- Honest source capture.
- Platform text drafts.
- Visual prompt files.
- Instagram cover and slide JSON prompt files.
- Actual rendered PNGs.
- A LinkedIn animated GIF.
- Preview notes.
- Image QA notes.
- A valid manifest.

## Skill

Primary skill:

```text
AIS-OS/.claude/skills/repurpose-youtube-video/
AIS-OS/.claude/skills/repurpose-youtube-video-v3/
```

Canonical workflow file:

```text
AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md
```

Use this file as the only execution checklist for full-package repurpose work.
Do not run multiple repurpose SOPs as competing checklists. If older deleted
SOP names appear in a prompt, ignore them and use this file.

Renderer and package builder:

```text
AIS-OS/tools/repurpose_full_package_builder.py
```

## Non-Negotiable Template Rule

The current approved template is the dense Stanley social template used after
the LinkedIn restart on 2026-07-05.

Do not replace it with a new style unless the user explicitly asks.

The template must keep:

- Cream graph-paper background.
- Stanley real avatar from `AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png`.
- Creator row with the current approved profile name and username. As of
  2026-07-30, render the profile name as `stanley chima`, render the
  username as `@chima-stanley-chukwu`, and store the LinkedIn URL separately
  in metadata: `https://www.linkedin.com/in/chima-stanley-chukwu/`.
- Strong standalone title.
- More subtext on intro slides and covers.
- Dense, useful teaching content.
- Clear module labels.
- Varied slide layouts.
- Actual PNG and GIF deliverables.

The goal is not decoration. The goal is a practical social post that teaches
one complete idea even if someone sees it without the caption.

## Source Analysis For LinkedIn And Social Posts

For LinkedIn/social posts, capture the strategy without copying the creator.

Record these fields in `source/source-brief.md`:

- Source link.
- Public accessibility status.
- Caption/body text summary.
- Attached image, GIF, or carousel summary.
- What the caption contributes that the image does not.
- What the image/GIF/carousel contributes that the caption does not.
- Creator/topic summary.
- Hook pattern.
- Trust mechanism.
- Visual pattern.
- Stanley recreation angle.
- Verified source facts.
- Missing or blocked source material.

Caption and image rule:

- Always analyze the caption/body text and the attached image, GIF, or carousel.
- Treat the caption as the primary source when it contains the full idea,
  framework, list, proof, CTA, or step-by-step explanation.
- Treat images as source evidence too: inspect layout, visible claims, numbers,
  diagrams, screenshots, proof, and how the caption and visual work together.
- Reject unrelated images before drafting. LinkedIn captures can include
  profile photos, repost thumbnails, side-feed images, or unrelated people-only
  images. Keep only visuals whose visible topic matches the caption/body; note
  rejected assets in `source/source-brief.md`.
- If the caption is complete and the image adds only presentation style, say so
  in `source/source-brief.md` and let the caption drive the repurpose.
- If the image contains the proof, numbers, screenshot, product state, or missing
  context, do not draft until that visual evidence is captured or honestly marked
  blocked.

If Firecrawl or public preview access is blocked, stop and ask for screenshots,
pasted text, or an authorized export unless Stanley accepts a
`source-brief-derived` package. Never invent a post body.

Use this recreation formula:

```text
Hook:
Name the repeated task, manual bottleneck, mistake, or workflow opportunity.

Context:
Describe the situation in plain English.

Mechanism:
Show how the AI workflow works.

Proof:
Use only a real source artifact, public detail, owned proof point, or safe
mechanism. Do not claim Stanley did the source creator's work.

Lesson:
Explain what the reader should now understand.

CTA:
Invite a DM, comment, bottleneck discussion, or workflow audit.
```

## Folder Contract

Every source gets this folder structure:

```text
AIS-OS/asset-folder/content/<slug>/
  source/
    transcript.txt
    source-brief.md
    original-url.txt
    render_social_images.py
  drafts/
    LinkedIn/
      images/
      text/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    Facebook/
      images/
      text/
  approved/
    LinkedIn/
      images/
      text/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    Facebook/
      images/
      text/
  published/
    LinkedIn/
      images/
      text/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    Facebook/
      images/
      text/
  preview/
    preview.md
    image-qa.md
  manifest.json
```

## Source Rules

Do not invent source content.

For any LinkedIn/social/blog/article/Substack/web URL, run Firecrawl before
drafting:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "<source-url>" `
  --out-dir "asset-folder/content/<slug>/source"
```

The wrapper auto-detects `http://localhost:3002` when the local self-hosted
Firecrawl server is running. This is the local-model path. Do not use the old
`webscraper` skill for v3 source capture.

Allowed source confidence values:

- `transcript-derived`
- `auto-caption-derived`
- `script-derived`
- `source-brief-derived`
- `caption-derived`
- `caption-and-image-derived`
- `public-preview-derived`
- `metadata-derived`

For YouTube:

1. Use `yt-dlp` or the approved scraper to fetch metadata and captions.
2. Save the cleaned transcript in `source/transcript.txt`.
3. Save source facts and safety notes in `source/source-brief.md`.

For LinkedIn/social posts:

1. Use public text, screenshots, pasted text, saved source briefs, and visible
   image/GIF/carousel evidence.
2. Analyze the caption/body and the attached visual before drafting.
3. If the caption contains the full framework, list, proof, and CTA, mark the
   package `caption-derived` or `public-preview-derived` and let the caption
   drive the repurpose.
4. If the visual adds essential proof or context, mark the package
   `caption-and-image-derived` only after that visual has been inspected.
5. If the full post is blocked, do not pretend it was scraped.
6. Mark the package `source-brief-derived` if only the local source brief is
   available.
7. Recreate the strategy for Stanley. Do not copy the creator's wording.

Public-facing copy rules:

- Keep `source/`, `manifest.json`, and QA files honest, but never tell the
  public audience that a post was repurposed, rewritten, based on a source,
  based on an article, or based on a lesson learned.
- Do not put phrases such as `the source says`, `the article explains`, `I
  repurposed this`, `lesson learned`, `lessons from`, or `from this content` in
  platform text, visual text, visual prompts, or Instagram JSON prompts.
- If the post is about a tool, model, app, platform, or automation system, name
  it at the top of the post and relevant visuals. Use `Claude Fable 5`,
  `Claude Code`, `ChatGPT`, `DaVinci Resolve`, `Firecrawl`, or the actual tool
  name instead of generic openers.
- When image code is used, save the exact code used to generate the images in
  the content package as `source/render_social_images.py`.

## Platform Purpose

LinkedIn:

- B2B trust.
- AI automation authority.
- Standalone framework or operating idea.
- Primary visual is `linkedin-animation.gif`.
- Static image and GIF must use the same content.
- Target clients in the USA, UK, Canada, and similar foreign markets.
- Make the business buyer clear: founder, operator, agency, marketing team,
  SaaS team, app company, e-commerce brand, or another company type.
- Tie the post to one business function that can be automated.

Instagram:

- Educational carousel.
- Slide 1 is an intro cover.
- The default 9-slide format uses slides 2-8 for dense teaching, proof, and
  CTA. Expand the count when the promise requires one slide per tool, step,
  role, case, or receipt.
- Each slide must make sense as a standalone post.

X:

- Standalone tweet-style posts.
- Every quote card must read as its own post.
- Do not make X feel like a continuation of a previous card.
- Write for the same B2B buyer as the LinkedIn post, but in a normal tweet
  voice. No labels such as `target audience` or `business function` should
  appear in the public tweet.

Facebook:

- Beginner-friendly AI learning and course-interest lane.
- Helpful and practical.
- No luxury, fake income, or desperate sales language.

## B2B Buyer Targeting Layer

For every LinkedIn/X business post, choose the buyer before writing the post.
The public post should not show these labels, but the draft should be guided by
them.

Required planning fields:

```text
Target audience:
Industry/company type:
Business function:
Department/owner:
Repeated task or deliverable:
Manual bottleneck:
Available input:
Automation angle:
Usable output or decision:
Faster/easier promise:
Proof/guardrail:
Business outcome:
CTA:
```

Default target audience:

- Companies, founders, marketing teams, agencies, SaaS teams, app companies,
  e-commerce brands, service businesses, and operators in the USA, UK, Canada,
  and similar foreign markets.

Default business functions to rotate:

- Marketing automation.
- UGC/ad video production.
- Google Ads campaign workflow.
- Content repurposing and publishing.
- Lead research and outbound prep.
- Sales follow-up.
- Reporting and dashboards.
- Client onboarding.
- Customer support workflows.
- Internal operations and handoff tasks.

Current direction:

- Every new post must solve, diagnose, or clarify a real company problem.
- Every new post must help a department or responsible role complete a repeated
  task, deliverable, or decision faster, easier, more consistently, or with
  clearer next steps.
- Content strategy, digital marketing, ad production, lead generation, sales,
  reporting, support, onboarding, and operational automation are valid lanes.
- Rotate beyond marketing when the source supports it: sales, finance,
  HR/recruiting, support, product, analytics, legal/procurement, and internal
  operations are valid department lanes.
- If the department, repeated task, friction, available input, mechanism,
  usable output, faster/easier promise, proof or guardrail, and outcome cannot
  be stated clearly, do not draft yet.

Default proof points Stanley can use:

- Claude content creation agentic system: reduced a client's app-promotion UGC
  production workflow from about one week to a few hours by handling the
  production pipeline end to end instead of requiring manual recording and
  editing for every asset.
- n8n Google Ads workflow: automates Google Ads campaign work.
- Additional proof points only after Stanley provides details.

Writing rule:

- Do not write generic AI education content when the goal is lead generation.
- Do not treat a model update, tool list, prompt list, skill list, or agent list
  as sufficient. Tie every item to work a department already needs to finish.
- Prefer the operational pattern `[familiar input] -> [workflow] -> [finished
  work product or decision]`.
- Make the reader think, `this person understands the workflow bottleneck in my
  company`.
- Do not claim fake metrics. If a number was not provided, explain the mechanism
  or likely business value without inventing results.
- End business posts with a soft CTA toward a workflow audit, bottleneck
  discussion, DM, or booked call.

## Required Media Count

A complete full package has exactly this minimum set:

LinkedIn:

```text
drafts/LinkedIn/images/linkedin-thumbnail.png
drafts/LinkedIn/images/linkedin-diagram.png
drafts/LinkedIn/images/linkedin-animation.gif
```

Instagram:

```text
drafts/Instagram/images/instagram-slide-01.png
drafts/Instagram/images/instagram-slide-02.png
drafts/Instagram/images/instagram-slide-03.png
drafts/Instagram/images/instagram-slide-04.png
drafts/Instagram/images/instagram-slide-05.png
drafts/Instagram/images/instagram-slide-06.png
drafts/Instagram/images/instagram-slide-07.png
drafts/Instagram/images/instagram-slide-08.png
drafts/Instagram/images/instagram-slide-09.png
```

X:

```text
drafts/X/images/x-thumbnail.png
drafts/X/images/x-quote-01.png
drafts/X/images/x-quote-02.png
drafts/X/images/x-quote-03.png
drafts/X/images/x-quote-04.png
drafts/X/images/x-quote-05.png
drafts/X/images/x-quote-06.png
drafts/X/images/x-quote.png
```

Facebook:

```text
drafts/Facebook/images/facebook-thumbnail.png
drafts/Facebook/images/facebook-course-card.png
```

Expected count:

- 21 PNGs.
- 1 GIF.
- LinkedIn GIF must have more than one frame.

## LinkedIn Template

LinkedIn is the first template to preserve exactly.

The static image and animated GIF must share the same content.

The GIF only changes one thing: it highlights one row per frame. The active
row must stand out with a bright theme accent color, usually orange for Claude
Skills/process posts. Do not use plain white as the active emphasis color.

LinkedIn image structure:

1. Cream graph-paper background.
2. Top badge that names the content type, such as:
   - `AI TEAM SYSTEM`
   - `EVERYDAY AI`
   - `CREATIVE OPS`
   - `VIDEO AUTOMATION`
   - `OUTCOME FIRST`
   - `REUSABLE AI`
   - `CONTENT SYSTEM`
   - `AI STACK`
3. Stanley creator row in the top-right.
4. Large standalone headline.
5. One accent line or accent word in orange.
6. Clear subtitle that explains the lesson.
7. Five labeled rows.
8. Dark bottom takeaway bar.

The title must stand alone.

Bad title:

```text
Prompt -> Skill -> Operating System
```

Good title:

```text
Stop Retyping AI Instructions
```

Bad title:

```text
Claude as a creative agency
```

Better title:

```text
A Creative Agency Is Really A Pipeline
```

Good LinkedIn row labels:

```text
1. RESEARCHER
2. STRATEGIST
3. COPYWRITER
4. EDITOR
5. QA REVIEWER
```

```text
1. OUTCOME
2. INSPECT
3. CHOOSE
4. RUN
5. VERIFY
```

```text
1. RESEARCH
2. TOOLS
3. SKILLS
4. QA
5. HANDOFF
```

Do not use the same generic five rows for every source.

Bad repeated rows:

```text
Spot the repeat
Give context
Create first pass
Add the gate
Save the system
```

Those rows are only acceptable if they truly fit the specific source. Otherwise
write source-specific labels.

## Instagram Carousel Template

### Locked Quality Standard From The Accepted Fable 5 Carousel

Use this standard for future Instagram carousel renders unless Stanley asks for
a different style.

Instagram is 3:4 or nothing:

- Canvas: `1080x1440`.
- Carousel length: 9 slides by default. Expand or contract only when the source
  and promise require it; keep the final slide for one CTA.
- Data beats design every time. Use checkable numbers, source facts, proof,
  or mechanisms over decorative design.
- Provide irresistible value for the audience. Do not make generic motivation.
- Every slide must look structurally different from the neighboring slides.
- Do not use a static or fixed main-body structure across the carousel. Shared
  brand chrome is fine, but the teaching area must be designed from the slide's
  meaning: leak meter, anatomy diagram, command menu, timeline, scanner,
  matrix, proof receipt, extraction flow, decision tree, or CTA panel.
- Do not let a new post inherit the previous post's teaching structure just
  because the renderer has reusable modules. Analyze the caption and image
  first, then build diagrams from the source's own shape: model map, effort
  dial, cost ladder, matrix, receipt, workflow loop, console, audit, or
  decision tree. Repeated visual structures across projects are a QA failure.
- Every slide after the cover must include a diagram, chart, map, process,
  comparison, receipt, proof block, QA gate, or CTA layout based on what that
  slide is about.
- If a slide needs a paragraph, split it into two slides.

Default 9-slide story:

```text
Slide 1: The hook
A bold claim plus a real number. This slide does 80% of the work and decides
the swipe.

Slide 2: The stakes
Why this matters right now. One sentence of context, zero throat clearing.

Slides 3-7: The value
One idea per slide. Big type, short lines, diagram-led.

Slide 8: The receipts
Proof it works. Use a screenshot, result, source fact, or number they can
check.

Slide 9: The CTA
One keyword to comment. The DM does the rest. Never two asks on one slide.
```

- Generate slide 1 from `cover-prompt.json`, not from the normal slide prompt.
- The cover must use the Premium Editorial cover system: cream engineering
  grid, huge dark navy headline, one orange highlighted line, small tool tag
  directly above the headline, subtitle directly below the headline, and the
  profile pill directly under the subtitle.
- The cover headline should be very large, about 60% of the canvas, and no more
  than three lines. If the title would exceed three lines, rewrite the title
  before rendering.
- Preserve exact user-provided cover title and subtext. Do not rewrite it unless
  Stanley asks.
- If Stanley does not provide cover subtext, write a specific summary of what
  the post is about. The subtext should give context for the title, not sound
  like a generic slogan. Good pattern: `This is how I would explain/use/build
  [tool/topic]: [specific angle].`
- Use Stanley's real avatar from
  `asset-folder/Brand_Assets/Stan Avatar.png`.
- Use `stanley chima` as the visible profile name.
- Use `@chima-stanley-chukwu` as the visible username unless Stanley gives a
  new username. Store `https://www.linkedin.com/in/chima-stanley-chukwu/` in
  JSON metadata as `profile_url`; do not render Markdown link syntax on the
  image.
- The profile tag on every Instagram teaching slide must use the same visual
  treatment as the cover profile pill: white rounded background, soft shadow,
  real avatar, name line, and visible `@` username line.
- For slides 2-9, move the first body section close to the title area. Do not
  leave a large empty band between the title/subtitle and the main section.
- Each slide must contain enough useful audience-facing information to work on
  its own, but never print creator instructions such as `stand alone`,
  `contain enough information`, `single post`, or `this slide should make
  sense` inside the actual image.
- Keep slide 6-style dense prompt slides when a prompt is useful, but do not
  force prompt boxes onto every slide. Use comparisons, workflows, route maps,
  cost maps, step systems, matrices, dashboards, ratios, or save-this summaries
  when those fit the content better.
- Always save the exact renderer used at
  `asset-folder/content/<slug>/source/render_social_images.py`.
- Regenerate the contact sheet after edits and visually inspect the cover plus
  slides before saying the package is done.
- Run or write a package-specific QA check after every render. It must verify
  required file counts, expected image dimensions, LinkedIn GIF frame count,
  and obvious layout risks such as cover title/subtitle overlap, clipped text,
  footer collisions, and repeated layouts. Save the report as
  `preview/image-qa.json` or document the checks in `preview/image-qa.md`.
- Final QA must be the last product step before handoff. After rendering and
  visual inspection, give an honest audience read: whether the cover/post is
  likely to stop the target audience or make them keep scrolling, what they
  will think/feel first, and the main reason. Do not give this judgment before
  inspecting the finished visuals.

Slide 1:

- Keep the intro style the user liked.
- Use a huge title of at most 6 words. If the natural title is longer, rewrite
  it before rendering.
- Use smaller subtext that briefly summarizes what the post is about.
- The cover should look like the approved reference covers:
  - cream graph-paper background,
  - small dark topic badge above the title,
  - huge dark navy title with one orange accent line or word,
  - concise summary subtext under the title,
  - Stanley profile pill under the subtext,
  - page count and swipe cue at the bottom.
- Do not turn slide 1 into a dense teaching slide.
- Do not reuse the same stacked-card teaching layout from slides 2-8 for the
  cover.
- For the cover image, follow `drafts/Instagram/images/cover-prompt.json`, not
  `slide-01-prompt.json`. `instagram-slide-01.png` is the cover render. The
  normal slide JSON prompts control the teaching slides after the cover.
- Do not render production labels such as `COVER PROMISE` on the public cover.
  Do not render `WHAT THIS POST TEACHES`, chip rows, prompt boxes, support
  cards, rule panels, workflow boxes, or dense teaching modules on the cover.
- The cover JSON prompt system is a premium editorial cover generator, not a
  teaching-slide generator. It should produce or guide a cover with a huge
  magazine-style headline, 1-3 highlighted words, fixed small top-left badge,
  fixed bottom-left profile pill, page counter, swipe cue, visible engineering
  grid, and generous intentional whitespace. Do not add support cards, rule
  panels, workflow boxes, or dense teaching modules to the cover unless the
  user explicitly asks.
- If Stanley says the cover text should be huge, treat that literally: the H1
  should cover about 60% of the canvas and use the cover JSON typography range
  (`150px` to `185px` on a 1080x1350 cover). Do not render cover titles at
  normal slide-heading size.
- Huge means gigantic enough to stop the scroll, visually closer to the
  accepted `Claude+Higgsfield Ai Agent` cover than to a normal title card. If
  auto-fit makes the title look merely large, force `cover_title_lines` and a
  `cover_font_size` around `190px` or higher on 1080x1440. Do not hand off a
  cover with a technically passing but visually weak title.
- Always run cover title QA after rendering. The package must record a PASS in
  `preview/image-qa.md` and `manifest.json` with:
  - `word_count <= 6`
  - `line_count <= 3`
  - `font_size >= 140`
  - `title_height_px >= 240`
  If any value fails, increase the title size, shorten the title, or rerender.
  Do not ask for approval until this QA passes.
- Cover title must be huge but no more than 3 lines. Place the tool tag
  directly above the title, not floating at the top of the canvas. Place the
  profile card directly under the subtitle. Keep the main cover content grouped
  in the center band of the image. Make the subtitle a little larger and bolder
  than normal body copy so it matches the premium cover reference.
- If Stanley provides exact cover title or subtext, preserve that wording
  exactly. Do not "improve", shorten, or rewrite user-provided cover copy
  unless Stanley explicitly asks for a rewrite.
- If Stanley does not provide exact subtext, make the cover subtitle a specific
  summary of the post. It should explain what the title means and what angle the
  post will teach.
- If Stanley provides a profile username or profile URL, apply it consistently
  to the cover and every slide. Public images should show the clean username
  text, not Markdown link syntax; keep any URL in JSON metadata or docs.
- Teaching slides must use the white space for actual audience-facing content:
  examples, steps, rules, checks, decisions, or workflows. Do not leave big
  empty areas just because the template has only two or three cards.
- Teaching-slide frame is fixed across future Stanley carousels unless he asks
  to change it: cream graph-paper background; real profile pill at the top
  right; circled slide number at the upper left; full-width pastel rounded
  title band immediately to the right of the number; one bold explanatory
  paragraph below; content-specific illustration in the middle; takeaway or
  supporting module beneath; page count at bottom left and swipe cue at bottom
  right. Only the illustration and its supporting modules are dynamic.
- Do not replace this fixed frame with small floating topic pills, role labels,
  generic output strips, or a different header placement. The reference
  package is `these-are-the-exact-claude-skills-i-use-every-day-v2` slides
  2-9. The profile display name remains `stanley chima` and the visible
  username remains `@chima-stanley-chukwu`.
- Density requirement: a teaching slide must fill its middle canvas with
  source-grounded explanation. Add the necessary decision criteria, examples,
  labels, process steps, checks, inputs, or outputs directly inside the
  content-specific illustration. Do not fill the area with decorative shapes
  or repeat the same generic `Output` statement. If a diagram is still easy to
  misunderstand in three seconds, enlarge it and add the missing explanation
  before adding another panel.
- Do not leave a large empty gap between the slide title/subtitle and the first
  content section. The body section should start directly under the title area
  with only normal breathing room.
- Never render internal instructions such as `contain enough information`,
  `stand alone`, `single post`, `this slide should make sense`, or similar QA
  notes into public images. Those belong in workflow docs only.
- Keep cover titles to three lines maximum unless Stanley explicitly asks
  otherwise. Place the tool tag directly above the title, place the profile
  pill directly under the subtitle, and center the full content block vertically
  in the image so it matches the Premium Editorial reference layout.

Working result from 2026-07-26:

- Bad cover: `Turn the prompt into a Skill` rendered with `WHAT THIS POST
  TEACHES` modules and chip rows. This looked like a teaching slide, not a
  cover.
- Correct cover: `Turn prompts into skills` with the subtext `Use the prompt
  that already works, save it as a narrow Claude Skill, and describe the exact
  task it should run.`
- Renderer fix: `tools/repurpose_full_package_builder.py` must render slide 1
  through the dedicated cover path only. The cover path must not draw
  `cover_cards`, chip rows, prompt boxes, or teaching modules.
- QA fix: `tools/repurpose_full_package_builder.py` must call
  `assert_cover_title_qa()` during build, write the metrics to
  `preview/image-qa.md`, and store `cover_title_qa` in `manifest.json`.
- Prompt fix: `drafts/Instagram/images/slide-01-cover-prompt.txt` must say
  huge title of at most 6 words plus brief summary subtext. It must explicitly
  forbid teaching cards, chip rows, prompt boxes, and what-this-teaches modules.

Reusable correction placeholders:

```text
Correction:
- Package: [CONTENT_SLUG]
- Slide: [SLIDE_NUMBER_OR_VISIBLE_MARKER]
- Problem: [WHAT LOOKED WRONG]
- Cause: [SOURCE-LEAKING COPY | WEAK COVER WEIGHT | TEXT OVERFLOW | VAGUE TERM | STATIC LAYOUT]
- Fix: [NEW COPY OR LAYOUT RULE]
- Renderer module: [MODULE_NAME]
- QA proof: [DIMENSIONS | COVER_WEIGHT | TEXT_INSIDE_CONTAINER | DYNAMIC_LAYOUT | NO_SOURCE_LEAK]
```

When a slide mentions `caption`, `source`, `repurpose`, `creator`, or another
internal production reference, rewrite it as audience-facing teaching copy
before rendering. The public viewer should never feel the slide was copied from
somewhere else.

When a term is not self-explanatory, such as `3-line header`, explain it on the
slide with plain placeholders: `[WHEN_TO_USE]`, `[INPUT_EXPECTED]`, and
`[OUTPUT_CREATED]`, or an equivalent audience-facing diagram.

Approved correction result from 2026-07-27:

- Package: `these-are-the-exact-claude-skills-i-use-every-day-v2`.
- Cover fix: title size was acceptable, but perceived weight was too light.
  Renderer must use a heavier/bolder title treatment, such as simulated
  overdraw, when Stanley says the cover is big enough but not bold enough.
- Slide source-leak fix: public slides must not say `caption`, `source`,
  `repurpose`, or anything that makes the viewer feel the post was copied from
  elsewhere. Rewrite those lines as direct audience-facing teaching.
- Diagram containment fix: result bands and bottom notes must use bounded text
  drawing or shorter copy so text never exits the diagram.
- Clarity fix: if a slide uses a technical phrase such as `Skill header`, define
  it immediately with plain placeholders. Approved pattern: `Header = when to
  use it, input expected, and output created`.
- QA proof required: inspect the full-size cover, the corrected slide, any slide
  with a bottom band, and the technical-explainer slide before calling the
  package done.

Slides 2-9:

- Must not all look the same.
- Must not all use prompt boxes.
- Must use most of the canvas.
- Must be full of useful information.
- Must follow the same source-derived argument.
- Must be understandable without the caption.
- Must use plain language.
- Must avoid jargon and vague AI words.
- Must each use a diagram or visual structure based on that slide's specific
  meaning. Do not reuse the same layout with changed text.
- Slide 9 must have one keyword CTA and no second ask.

Use different modules based on the actual lesson:

- `STAKES` when showing why the issue matters now.
- `ROUTING` when showing how a description triggers a skill or workflow.
- `ONE_JOB` when comparing broad vs narrow workflow design.
- `BUILD_LOOP` when showing a repeatable loop.
- `RECEIPTS` when showing proof, result, source facts, or checkable claims.
- `CTA` when showing the final comment keyword.
- `PROMPT` when the viewer should copy a prompt.
- `TIPS` when giving tactical advice.
- `INSTRUCTION` when giving a rule to follow.
- `TECH STACK` when showing tools, connectors, models, files, or surfaces.
- `CHECKLIST` when listing review items.
- `QA GATE` when showing pass/fail checks.
- `WORKFLOW` when showing stages.
- `ROLES` when showing responsibilities.
- `OUTPUT` when showing deliverables.
- `TOOLS` when listing tooling layers.
- `SAVE THIS` when giving a recap.

If the module is a prompt, label it `PROMPT`.

If the module is a tip, label it `TIPS`.

If the module is an instruction, label it `INSTRUCTION`.

Do not use `APPLY THIS` as the default label.

Do not leave large empty white space. Add:

- Comparison cards.
- Checklist rows.
- Tool stack rows.
- Before/after blocks.
- Prompt panels.
- QA gates.
- Mini workflow maps.
- Output examples.
- Mistake/fix pairs.
- Role cards.
- Decision filters.

## X Template

X visuals are tweet-style standalone posts.

Each X card must:

- Make sense by itself.
- Not depend on another card.
- Use Stanley avatar, name, verified badge, and handle.
- Use one clean thought.
- Avoid labels like `LESSON`, `TIP`, or `Standalone post`.
- Avoid fake engagement rows.
- Avoid timestamps.
- Avoid slide counters.

Bad X card:

```text
3/ This is why the next step matters...
```

Good X card:

```text
The prompt is not the asset. The repeatable workflow is.
```

## Text Draft Rules

Create these files:

```text
drafts/LinkedIn/text/post.txt
drafts/Instagram/text/post.txt
drafts/Instagram/text/caption.txt
drafts/X/text/post.txt
drafts/X/text/thread.txt
drafts/Facebook/text/post.txt
drafts/Facebook/text/caption.txt
```

Each draft must:

- Start with a strong hook.
- Captions must start with a scroll-stopping hook. A playful unrelated hook is
  allowed if it immediately apologizes and pivots into the post.
- Track the source material.
- Avoid fake ownership claims.
- Avoid fake revenue or client proof.
- Use short lines.
- Explain jargon.
- Make sense to a normal reader.

## Dumb-Model Execution Steps

Follow these steps in order.

1. Read the user request.
2. Read this SOP.
3. Do not read or follow any other repurpose SOP. This is the only execution
   checklist.
4. Read platform rules and visual recipes only if you need platform voice or
   image recipe detail.
5. Identify whether the source is YouTube, LinkedIn, script, transcript, or
   source brief.
6. Capture the source honestly. For social posts, analyze both caption/body and
   attached images/GIFs/carousels before drafting.
7. Create or reuse `AIS-OS/asset-folder/content/<slug>/`.
8. Save `source/transcript.txt`.
9. Save `source/source-brief.md`.
10. Save `source/original-url.txt`.
11. Write platform text drafts.
12. Humanize the drafts.
13. Write visual prompt files.
14. Generate Instagram JSON prompt files:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/generate_instagram_json_prompts.py `
  --run-dir "asset-folder/content/<slug>"
```

15. Confirm `cover-prompt.json`, `slide-blueprint.json`, and each
    `slide-XX-prompt.json` exists in `drafts/Instagram/images/`.
16. Build source-specific visual data. Do not reuse generic slide text.
17. Render LinkedIn PNG and GIF first.
18. Confirm LinkedIn static image and GIF have the same content, and confirm
    the GIF active row uses a bright theme accent color rather than a white
    emphasis row.
19. Render Instagram carousel.
20. Confirm slide 1 has a huge title of at most 6 words, concise summary
    subtext, a real number or numeric proof point, no teaching cards, no chip
    rows, and no prompt/module panels.
21. Confirm every Instagram slide is `1080x1440` and the rendered count matches
    the approved slide blueprint. Use 9 slides by default.
22. Confirm all teaching slides are structurally different from their
    neighbors and each has a diagram based on the slide meaning.
23. Confirm the final slide has one keyword CTA and the Instagram caption ends
    with the keyword CTA as the final ask.
24. Render X cards.
25. Confirm every X card stands alone.
26. Render Facebook visuals.
27. Create `preview/preview.md`.
28. Create `preview/image-qa.md`.
29. Update `manifest.json`.
30. Count media.
31. Inspect representative images.
32. Fix any layout, clipping, ambiguity, repeated module, or blank-space issue.
33. Rerender after fixes.
34. Ask the user what to approve next.

## Verification Commands

Run from:

```text
C:\Users\DELL\Master Project\Stan OS
```

Count PNGs:

```powershell
(Get-ChildItem -LiteralPath "AIS-OS/asset-folder/content/<slug>/drafts" -Recurse -Filter *.png | Measure-Object).Count
```

Count GIFs:

```powershell
(Get-ChildItem -LiteralPath "AIS-OS/asset-folder/content/<slug>/drafts" -Recurse -Filter *.gif | Measure-Object).Count
```

Check GIF frames:

```powershell
$env:PYTHONUTF8='1'
python -c "from PIL import Image; p=r'AIS-OS/asset-folder/content/<slug>/drafts/LinkedIn/images/linkedin-animation.gif'; im=Image.open(p); print(getattr(im,'n_frames',1), im.size)"
```

Validate manifest:

```powershell
python -m json.tool "AIS-OS/asset-folder/content/<slug>/manifest.json"
python -m json.tool "AIS-OS/asset-folder/content/<slug>/drafts/Instagram/images/cover-prompt.json"
python -m json.tool "AIS-OS/asset-folder/content/<slug>/drafts/Instagram/images/slide-blueprint.json"
```

Search stale placeholders:

```powershell
rg -n "Replace this placeholder|PNG generation is pending|No PNGs|images_pending|Draft$|Visual Prompt$|APPLY THIS" "AIS-OS/asset-folder/content/<slug>"
```

Expected:

- PNG count is at least 21.
- GIF count is at least 1.
- LinkedIn GIF has more than one frame.
- Manifest JSON is valid.
- Instagram cover and slide JSON prompt files are valid.
- Placeholder search has no matches.

## Visual QA Checklist

Before calling a package done, answer yes to every item:

- Did I run `.agents/skills/repurpose-post-qa-agent/SKILL.md` as the final gate?
- Does `preview/post-qa-agent-report.md` score at least 90/100 with no hard
  fails and a `LIKELY TO STOP` audience verdict?
- Did I use the approved Stanley template?
- Did I use Stanley's real avatar?
- Did I avoid a fake or fallback avatar?
- Does LinkedIn stand alone as one complete post?
- Does LinkedIn PNG match LinkedIn GIF content?
- Does LinkedIn GIF highlight one row per frame with a bright theme accent
  color, not a white emphasis row?
- Does Instagram slide 1 have enough subtext and a real number or numeric proof
  point?
- When the cover needs explanatory subtext, is the subtext 3-4 readable lines
  that explain the post, not a tiny slogan?
- Does every Instagram slide use `1080x1440`, and does the count match the
  approved source-specific blueprint?
- Do Instagram slides 2-9 use varied layouts?
- Are the main teaching structures dynamic, with no neighboring slides using
  the same diagram/container arrangement with only swapped text?
- Does every slide after the cover use a diagram based on that slide's
  meaning?
- Does the final slide use one keyword CTA only?
- Does the Instagram caption start with a strong natural hook?
- Does the Instagram caption end with the keyword CTA as the final ask?
- Does every Instagram/Facebook caption have a real structure: natural
  strong hook, why it matters, useful body/framework, proof or checkable detail,
  and one final keyword CTA when a keyword is used?
- Is each generated caption about 70% similar to the reference caption's
  structure and core content, preserving the same sequence, claim, examples,
  proof, and ask where safe while paraphrasing into Stanley's voice?
- Did I reject captions that are only summaries, loose notes, or generic
  "save this" endings?
- Do different projects use different slide order and structure when the source
  calls for it?
- Did I avoid using a prompt box on every slide?
- Are module labels accurate?
- Did I avoid internal QA/helper text inside public visuals, such as `this
  slide should make sense`?
- Does every prompt box say `PROMPT`?
- Does every tips box say `TIPS`?
- Does every instruction box say `INSTRUCTION`?
- Last step: did I inspect the finished visual and give Stanley an honest
  audience-stop/scroll judgment with the likely first thought or feeling?
- Does every X card stand alone?
- Is the text readable?
- Did I check for low-contrast color on light cards or white panels, especially
  colored titles, borders, chips, and diagram labels?
- Did I read every visible sentence on the final PNG/contact sheet and fix any
  incomplete sentence, clipped line, or text escaping its box?
- Did I open any flagged slide individually after the contact sheet, not only
  trust the sheet?
- Is the source relationship honest?
- Did I avoid fake ownership claims?
- Did I avoid fake metrics?
- Did I avoid large empty white space?
- Did I inspect representative PNGs?
- Did I specifically check that the cover title does not cut into the subtitle?
- Did I check that titles, subtitles, body sections, profile rows, and footers
  do not overlap or clip on every contact sheet image?
- Did I validate counts and manifest?

If any answer is no, the package is not done.

Any edit to public copy, a slide, GIF, PDF, caption, or derivative invalidates
the previous QA. Rerender affected media, rebuild derivatives, rerun the
technical audit, reinspect the changed output at full size, and update
`preview/post-qa-agent-report.md` before handoff.

## Failure Log

### Failure: The workflow became too generic

What happened:

The renderer reused the same five rows for every source:

```text
Spot the repeat
Give context
Create first pass
Add the gate
Save the system
```

Why this failed:

The images looked like a continuation of one generic post instead of standalone
source-specific posts.

Fix:

Create source-specific title, subtitle, five row labels, row body text, and
bottom takeaway for each package.

### Failure: LinkedIn title did not make sense alone

What happened:

Some titles described the internal repurposing idea instead of teaching a
reader.

Fix:

Rewrite every LinkedIn title as a standalone lesson:

- `Stop Running Your Content Team Manually`
- `Start With The Task You Repeat Every Week`
- `A Creative Agency Is Really A Pipeline`
- `Edit Video With Plain English`
- `Give AI The Outcome, Not The Steps`
- `Stop Retyping AI Instructions`
- `A Channel Is A Workflow, Not A Video Idea`
- `A Chatbot Is Not An Operating System`

### Failure: LinkedIn image and GIF could drift

What happened:

The static image and animation could be treated as separate assets.

Fix:

Use the same content data for both. The GIF only highlights one row per frame,
using a bright theme accent color such as orange for the active row.

### Failure: Carousel had too much white space

What happened:

Slides were sparse and looked plain.

Fix:

Use the empty space with useful content: subtext, cards, checklists, tech stack,
prompt panels, workflow rows, QA gates, output examples, and tips.

### Failure: Slides looked the same

What happened:

The same layout and lower module repeated across slides.

Fix:

Choose the module based on the slide's purpose. Use prompt only when a prompt is
actually needed.

Do not only vary the text. Vary the structure and order per project when the
source calls for it. Example: a faceless YouTube system can use production-line
order, while Claude Code can use inspect/plan/execute/edit/verify order.

Reusable enforcement rule:

- Before rendering, write a slide map that assigns every slide one job:
  `hook`, `stakes`, `tool/process value`, `proof/receipt`, or `single CTA`.
- For a tool library, one tool slide must show the tool name, what it does, and
  the process or usable output. Do not reduce the teaching area to a generic
  sentence plus an ornamental icon.
- Do not approve a carousel when three or more slides share the same header,
  profile row, body container, and result-strip composition. Shared brand
  chrome is allowed; the main teaching shell is not.
- When a repeated lower `Output` strip, card grid, profile bar, or label makes
  the deck feel templated, replace it with a meaning-specific module such as a
  scorecard, anatomy map, language flow, alert meter, ranked board, storyboard,
  handoff form, branching tree, platform split, receipt, or CTA panel.
- The QA report must name the selected structure for every slide and mark the
  package `REVISE` if the cover is generic, familiar to an existing Stanley
  post, not task/problem/outcome-led, merely large rather than gigantic, or
  fails full-size title containment.

Cover correction placeholders:

```text
Correction:
- Package: [CONTENT_SLUG]
- Slide: [SLIDE_NUMBER_OR_VISIBLE_MARKER]
- Problem: [GENERIC_OR_DUPLICATE_COVER_PROMISE | WEAK_COVER_WEIGHT | TITLE_OVERFLOW]
- Cause: [TITLE_NOT_TASK_LED | REUSED_PROMISE | AUTO_FIT | INSUFFICIENT_WEIGHT]
- Fix: [SHORTER_TASK_PROBLEM_TITLE | THREE_LINE_LAYOUT | HEAVIER_RENDER | NEW_SUBTEXT]
- Renderer module: [MODULE_NAME]
- QA proof: [FULL_SIZE_INSPECTION | SAFE_WIDTH | TITLE_HEIGHT | DISTINCT_PROMISE]
```

### Failure: Public visuals included internal helper text

What happened:

Some slides contained agent/QA language such as:

```text
This slide should make sense even if someone sees it without the rest of the
carousel.
```

Why this failed:

That sentence is an instruction for the creator, not content for the audience.

Fix:

Never render internal QA, implementation notes, or meta-instructions into the
public image. Convert them into audience-facing labels such as `RESULT`,
`BETTER MOVE`, `RIGHT WAY`, `SAVE THIS`, or remove the panel.

### Failure: Captions had no hook

What happened:

Captions started with plain explanation and did not stop the scroll.

Fix:

Start every Instagram and Facebook caption with a hook. Hooks may be playful,
dramatic, or slightly unrelated, but must quickly apologize or pivot back into
the post. Examples:

```text
You have 20 unread messages.

Sorry, that was not part of the post. I just needed your attention because...
```

```text
I bet this will blow your mind.

Sorry for the dramatic hook, but...
```

```text
You have never seen this before.

Okay, that hook was loud. But...
```

### Failure: X cards felt like a sequence

What happened:

Some X content read like part of a thread instead of a standalone post.

Fix:

Write each X card as one complete thought.

### Failure: QA notes were too weak

What happened:

The package said images were done because files existed.

Fix:

Open contact sheets and representative images. Verify text, spacing, avatar,
standalone meaning, module labels, and clipping.

### Failure: Disk filled during rerender

What happened:

The C: drive hit 0 bytes free during a metadata refresh.

Fix:

Before heavy rendering, check:

```powershell
Get-PSDrive -PSProvider FileSystem
```

Clear only safe workspace temp files if needed:

```text
AIS-OS/.tmp/
```

Do not delete deliverables.

## Current Corrected LinkedIn Packages

The LinkedIn restart was applied to:

- `how-to-use-ai-save-time`
- `how-i-use-ai-to-save-10-hours-per-week`
- `higgsfield-claude-creative-agency`
- `claude-in-davinci-resolve-video-editing-agent`
- `claude-code-video-editing-wow-moment`
- `claude-skills-one-line-prompt-system`
- `automated-faceless-youtube-system-teardown`
- `claude-stack-plugins-skills-and-mcps`

Contact sheet used for QA:

```text
AIS-OS/.tmp/linkedin-revised-contact-sheet.png
```

## Final Rule

Do not call a package complete because the file count is correct.

The package is complete only when the content is source-derived, standalone,
readable, dense, varied, visually inspected, and saved in the required folder
contract.
