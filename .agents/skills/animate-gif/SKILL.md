---
name: animate-gif
description: Create short looping animated GIFs for social media posts, especially node-flow, stack-map, workflow-map, and signal-through-cards visuals where lines light up and cards glow one by one. Use when the user asks for a GIF instead of a static image or video, asks to recreate LinkedIn-style animated diagrams, wants loading-light animations through nodes, or needs editable/configurable social visuals for AI automation content.
---

# Animate GIF

## Overview

Create lightweight animated GIFs that behave like social post visuals: a clean
diagram, a moving signal, and nodes that light up as the signal reaches them.
Use this skill when the output should be a GIF, not a video and not a flat PNG.

## Core Workflow

1. Define the message before drawing.
   - What system is being shown?
   - What moves through the system?
   - What should light up first, second, and last?
2. Choose the GIF pattern:
   - node-flow stack
   - before/after process
   - command-to-output pipeline
   - checklist activation
   - client workflow map
3. Write a JSON config with title, subtitle, columns, colors, and node labels.
4. Render the GIF with `scripts/render_node_flow_gif.py`.
5. Render or save a poster PNG beside the GIF for previews and fallback images.
6. Check the GIF visually before handoff.

## Node-Flow GIF

Use node-flow GIFs for visuals like:

- AI stack maps.
- Codex or agent tool chains.
- Client automation systems.
- CRM/reporting/content workflows.
- MCP, app, and skill diagrams.

The signal should move from the top control node into each group, then through
the cards. When the signal reaches a card, that card should glow, brighten, or
gain a visible active state.

Run:

```powershell
$py = "C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe"
& $py "AIS-OS\.Codex\skills\animate-gif\scripts\render_node_flow_gif.py" `
  --config "path\to\stack-config.json" `
  --output "path\to\stack.gif" `
  --poster "path\to\stack-poster.png"
```

Read `references/node-flow-gif.md` when designing a new config.

## Social Rules

- Keep GIFs short: 4 to 8 seconds.
- Use 1080x1350 for LinkedIn/Instagram portrait posts unless the user asks for
  another size.
- Use fewer words inside cards than a static carousel would use.
- Put detailed explanation in the caption, not inside the GIF.
- Prefer clean business diagrams over cinematic effects.
- Always create a poster PNG fallback when possible.
- Never copy another creator's exact graphic labels unless the user owns the
  source or provides permission. Recreate the pattern using the user's own
  offer, workflow, and proof.

## Output Contract

Save GIF outputs inside the relevant content package:

```text
AIS-OS/asset-folder/content/<slug>/drafts/<Platform>/images/
  <name>.gif
  <name>-poster.png
  <name>-config.json
  visual-prompt.txt
```

If the GIF is for a multi-platform package, put the master GIF in the LinkedIn
image folder and reuse/adapt it for other platforms only when the format fits.

## QA Checklist

- The GIF opens and loops.
- The first frame reads clearly as a social graphic.
- The light visibly travels through lines or cards.
- Each reached node has an active state.
- Text is readable at mobile size.
- The GIF file size is acceptable for social upload.
- The content uses the user's own positioning and does not duplicate a
  reference creator's exact post.
