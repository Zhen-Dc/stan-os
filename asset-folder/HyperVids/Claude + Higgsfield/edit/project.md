## Session 1 - 2026-07-21

**Strategy:** Use the provided script as the source of truth, use ElevenLabs Scribe only for word-level timing, and remove dead spaces, false starts, and repeated bad takes from `Script 2.mov`.

**Decisions:** Dropped the false starts at 3.96, 17.44, 21.96, 53.46, 56.00, 78.52, 101.70, 104.44/109.74 duplicates where cleaner script-matching pieces were available, and the trailing "all over" after "starts the process again".

**Reasoning log:** The finished EDL prioritizes matching the pasted script over preserving every recorded phrase.

**Outstanding:** HyperFrames visual overlays can be added after this base dead-space edit is approved.

## Session 2 - 2026-07-21

**Strategy:** Rebuild the edit as sentence-safe because the first pass cut too tightly around individual words and damaged spoken sentence flow.

**Decisions:** Replace the micro-stitches around product analysis, ad breakdown, editor actions, reporting, and the learning-loop sentence with longer complete spoken ranges. The v2 EDL favors natural complete delivery over forcing every script word through a hard splice.

**Reasoning log:** When the recording contains a mistake, a complete alternate spoken phrase is safer than stitching small word fragments that sound clipped.

**Completed:** Rendered `final-v2-sentence-safe.mp4`, updated the HyperFrames timeline source, linted the HyperFrames project with zero errors, and opened the preview server on port 3019.
