# Node-Flow GIF Reference

Use this pattern when a post should feel like a live system diagram.

## Best Uses

- AI automation stacks.
- Agent workflows.
- MCP and app connection maps.
- Business process automation maps.
- Client onboarding or reporting pipelines.

## Config Shape

```json
{
  "title": "My AI Automation Stack",
  "subtitle": "Stanley | AI automation systems",
  "center_label": "AI OPS",
  "footer": "The tools matter less than the chain.",
  "columns": [
    {
      "title": "WORKFLOWS",
      "subtitle": "8 mapped",
      "color": "#2FA8FF",
      "nodes": [
        {"title": "Lead research", "meta": "Finds the right accounts"}
      ]
    }
  ]
}
```

Use three columns for the Charlie Hills-style stack map. Use two columns for a
before/after process. Use one column for a simple vertical pipeline.

## Copy Rules

Keep each card short:

- title: 2 to 4 words
- meta: 3 to 8 words

Good:

```text
Lead research
Finds the right accounts
```

Too long:

```text
This workflow searches the internet, enriches leads, qualifies prospects, and
then drafts the outreach message.
```

## Motion Rules

- Start with the center node active.
- Light column headers next.
- Light cards in row order.
- Leave reached cards softly active so the viewer sees progress.
- Use a brighter glow only for the current row.
- End with every node active for a beat before looping.

## Visual Rules

- White or very light grid background.
- Navy headline with one warm accent word when useful.
- Blue, orange, and purple columns work well for stack diagrams.
- Use rounded cards with small icons or badges only when they do not crowd text.
- Put the business lesson in the post text, not as a paragraph inside the GIF.
