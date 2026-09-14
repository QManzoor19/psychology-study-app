# Study loop

A five-step loop per lesson. Steps 1, 3 and 5 need Claude; steps 2 and 4 do not.

| # | Step | Where |
|---|------|-------|
| 1 | **Pretest** — answer 5 questions on a lesson you have *not* read. Expect to fail. | `pretest/<lesson>.md` |
| 2 | **Read once**, closed book afterwards. No notes while reading. | `psychology.html` |
| 3 | **Blurt** — write what you remember into a session file, then ask Claude to mark it. | `sessions/` |
| 4 | **Targeted questions** on the gaps only — not the whole lesson. | Claude generates |
| 5 | **Schedule** by *category* of error, not by lesson. | `state.json` |

## Running it

Say to Claude, in this directory:

- `pretest 5.1` — generates the prequestions if they don't exist, then shows them
- `mark my blurt on 5.1` — after you have written into a session file
- `what's due` — reads `state.json` and tells you today's set
- `drill definitions` — questions across every lesson on your weakest category

## The unit of recall

These notes are argument-shaped: *claim → evidence → objection → current status*. So rubrics
score arguments, not just terms. "Reconstruct the case for the neuron doctrine" is the right
prompt; "define synapse" is a warm-up.

## Categories

Every rubric line is tagged with one, and `state.json` tracks them separately, because the
useful finding is not "you scored 60% on 5.1" but "you lose the evaluation half of every lesson".

`definition` · `structure` · `mechanism` · `number` · `study` · `application` · `correction`
