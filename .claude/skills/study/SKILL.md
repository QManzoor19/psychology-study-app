---
name: study
description: Run the retrieval study loop on a psychology lesson - pretest before reading, mark a closed-book blurt against the lesson rubric, generate gap-targeted questions, and update the spaced schedule in study/state.json. Use when the user says "pretest 5.1", "mark my blurt", "what's due", or "drill <category>".
---

# Study loop

State lives in `study/state.json`. Lesson text lives in the `NOTES` object in
`psychology.html`, keyed as in `study/state.json` (e.g. `5.1` → `b-neuron`).

## pretest <lesson>
If `study/pretest/<lesson>.md` exists, show it. Otherwise read the lesson from `NOTES`,
write 5 questions answerable only from that lesson, put the answers in a collapsed
`<details>` block at the foot, save, then show it. Do not reveal answers in the chat.

## mark <lesson>
1. Read the newest file in `study/sessions/` for that lesson, or ask the user to paste
   their blurt.
2. Read `study/rubrics/<lesson>.md`. If absent, build it from `NOTES` first: one line per
   recallable item, each tagged with a category.
3. Mark every rubric line got / partial / missed. Never mark from memory of the lesson -
   read it.
4. Report in this order: score by category, got (brief), missed (quoted from the rubric,
   tagged), **wrong** (confidently stated errors, separately - these matter more than blanks),
   the pattern across categories, next due date.
5. Append the marking to the session file and update `study/state.json`:
   `by_category`, `category_totals`, `interval_index`, `due`.

## Scheduling
Intervals: 1, 3, 7, 16, 35 days. Advance one step if the score is >= 80% **and** nothing was
in the wrong list. Otherwise reset to index 0. Schedule by category as well as by lesson:
if a category is below 60% across three or more lessons, say so and offer a cross-lesson drill.

## drill <category>
Pull every rubric line with that tag across all rubrics, and generate questions from the
lines the user has missed before, in preference to ones they have not seen.

## Rules
- Free recall is the point. Never show the lesson text before the user has written.
- Mark honestly. A generous mark destroys the value of the record.
- Confidently wrong is worse than blank, and is reported separately.
