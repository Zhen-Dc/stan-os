# Decisions Log

Append-only record of meaningful decisions and why they were made. `/level-up` Phase 2 (Method interview) writes scoped automation specs here. You can also append manually whenever you decide something worth remembering.

**Format per entry:**

```
## YYYY-MM-DD — Short title

**Decision:** what was decided.

**Why:** the reasoning, constraints, and what would change your mind.

**Alternatives considered:** what else was on the table.

**Owner:** who's accountable.
```

Keep it terse. Future-you will thank present-you for capturing the *why*, not just the *what*.

---

## 2026-06-25 — Adopt WAT framework for AIS-OS execution

**Decision:** Add the WAT framework to Stanley's AIS-OS: `workflows/` for Markdown SOPs, `tools/` for deterministic scripts, and `.tmp/` for disposable processing files.

**Why:** Stanley's OS needs reliable execution for research, automation, content operations, and client workflows. Separating workflows, agent coordination, and tools keeps reasoning flexible while making repeatable tasks more dependable.

**Alternatives considered:** Keep all instructions inside `CLAUDE.md` only, or use ad hoc scripts without documented workflows.

**Owner:** Stanley Chima.
