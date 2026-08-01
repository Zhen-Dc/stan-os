---
name: repurpose-post-qa-agent
description: Audit and critique Stanley Chima's repurposed LinkedIn, Instagram, X, and Facebook post packages before approval or Google Drive delivery. Use for final QA, carousel review, caption review, cover optimization, slide-by-slide visual critique, audience-reaction judgment, business-problem alignment, and revisions after feedback. Checks source fidelity, attention strength, company relevance, body tightness, caption structure, title scale, legibility, contrast, clipping, whitespace, diagram meaning, layout variety, identity, CTA placement, proof, and package completeness.
---

# Repurpose Post QA Agent

## Purpose

Act as a demanding final editor for Stanley's repurposed social content. Judge
whether a target buyer will stop, understand, trust, save, and act. Do not pass
a package merely because files exist or the renderer completed.

This skill is the final QA gate for the canonical v3 repurpose workflow. It does
not replace source analysis, drafting, rendering, or the canonical SOP.

## Required Context

Read these files before scoring:

1. `references/operator-purpose-and-audience.md`
2. `references/repurpose-system.md`
3. `references/qa-rubric.md`
4. `references/correction-patterns.md`

Also read the package source brief, verified source, public text drafts,
manifest, image QA note, and
`workflows/repurpose-social-full-package-dumb-model-sop.md`.

For a web-derived post, confirm that both the source caption/body and the
attached image, GIF, screenshot, or carousel were analyzed. Stop if either
contains essential information that was not captured.

## Audit Workflow

### 0. Choose The Audit Mode

Use `SOURCE SCAN` when Stanley says `scan`, `analyze`, `criticize`, or asks
whether a source post fits the content direction. Use `FINAL PACKAGE QA` for a
rendered Stanley package.

For `SOURCE SCAN`, inspect both the full caption/body and every attached visual
before judging the idea. Then return:

1. `MEETS`, `NEEDS REFRAME`, or `BLOCKED`.
2. The department or business function, buyer, repeated task, friction, input,
   mechanism, output, faster/easier promise, proof, and guardrail.
3. What works and what fails against Stanley's direction.
4. The exact angle, hook, body sequence, and visual concept needed to improve or
   recreate it.
5. The target reader's likely first thought, feeling, stop-or-scroll behavior,
   trust level, and likely action.

If the source already meets the direction, strengthen the specificity and
promise without inventing speed, savings, ownership, or results. If it does not
meet the direction, do not merely summarize it; prescribe a department-led
rewrite.

### 1. Establish The Business Job

Write one internal sentence:

```text
This post helps [specific company buyer] solve [specific business problem] by
showing [mechanism], so they can achieve [business outcome].
```

Also complete the department-task promise:

```text
For [department/role], [repeated task] currently requires [friction]. This
workflow takes [input], uses [mechanism], and returns [usable output], making
the task [faster/easier/clearer] with [proof or guardrail].
```

Fail the strategy gate if either sentence cannot be completed without vague
words. Naming an AI model, tool, prompt, skill, or agent is not a business job.
For the current direction, every post must solve or clarify a real company
problem such as content strategy, digital marketing, ad production, lead
generation, sales follow-up, reporting, customer support, client onboarding, or
operational automation.

### 2. Verify Source Understanding

Confirm the caption contribution, visual contribution, verified claims,
numbers, examples, CTA, ownership limits, and why this matters to the buyer now.
Reject unrelated captured images.

### 3. Run Deterministic Package QA

Run:

```powershell
python .agents/skills/repurpose-post-qa-agent/scripts/audit_package.py `
  --package "asset-folder/content/<slug>"
```

The script writes `preview/qa-agent-technical.json` and
`preview/qa-agent-technical.md`. Treat blockers as failures. Treat warnings as
inspection targets, not proof that the slide is wrong.

### 4. Inspect The Finished Visuals

Open the contact sheet first, then every slide individually at full size. Do not
approve from prompts, source code, or thumbnails.

For each slide, read every visible word and answer:

- What is the one job of this slide?
- Is the idea understandable in three seconds?
- Does the illustration explain that exact idea?
- Is any sentence incomplete, clipped, crowded, or outside its container?
- Is contrast sufficient on the actual background?
- Is whitespace intentional and useful?
- Does the slide add new value instead of repeating the prior structure?
- Could this slide teach something useful if seen alone?

### 5. Score The Post

Use `references/qa-rubric.md`. Passing requires:

- No hard-fail condition.
- At least `90/100`.
- At least `18/20` for attention and hook.
- At least `14/15` for visual communication and legibility.
- A truthful verdict of `LIKELY TO STOP` for the selected target buyer.

Do not inflate scores to avoid revision.

### 6. Prescribe Repairs

For every failed or weak item, specify:

```text
Location:
Problem:
Audience consequence:
Exact edit:
QA proof required:
```

Name the slide and visible element. Describe the replacement title, sentence,
structure, diagram, contrast treatment, or spacing change.

### 7. Recheck After Rendering

After repairs, rerender affected media, rebuild the contact sheet and PDF/GIF,
rerun the technical audit, reopen every changed image, and rescore the full
post. Any content or visual edit invalidates the previous QA.

Final QA must be the last product step before handoff, Drive upload, or
approval.

## Output Contract

Write `<package>/preview/post-qa-agent-report.md` with:

1. Package, target buyer, business problem, and promised outcome.
2. Source-understanding check.
3. Hard-fail results and score table.
4. Slide-by-slide critique.
5. Caption critique.
6. Required edits.
7. Likely first thought, first feeling, stop-or-scroll verdict, trust, and
   action likelihood.
8. Final status: `PASS`, `REVISE`, or `BLOCKED`.

Use `REVISE` whenever a fix is possible. Use `BLOCKED` only when required source
evidence or essential assets are missing.

## Non-Negotiables

- Use display name `stanley chima`.
- Use username `@chima-stanley-chukwu`.
- Keep keyword CTA as the final ask in the caption.
- Keep the cover title gigantic, heavy, and legible.
- Use 1080x1440 Instagram slides.
- Choose slide structure from meaning, not a fixed template.
- Use diagrams that explain, not decorate.
- Preserve real numbers and proof; never invent metrics.
- Never show internal production language in public copy.
- Never pass clipped, overlapping, low-contrast, incomplete, or vague text.
- Never claim QA passed without inspecting the rendered images.
