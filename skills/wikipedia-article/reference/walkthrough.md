# walkthrough — Step by step through the findings

Interactive companion to `audit` and `revise`. Instead of a batch fix run, you walk through the findings one at a time with the writer: show the diff, discuss it, sharpen it, then apply, change, or skip. Also the mode for preparing edits to a **live article** — with a Go/No-Go check before anything is transferred.

The conversation happens in the writer's language. You propose; the writer decides. Never apply ahead of a decision, never batch two steps into one.

## When

- After an audit, when the writer wants to discuss each fix individually instead of a batch `revise`.
- When the target is a live article and edits must be prepared against the current live state.

## Two contexts

- **Draft walkthrough** — base is the local draft file. Findings come from the audit (their stable IDs, F1, F2, …).
- **Live walkthrough** — base is the article's live wikitext. Findings come from an audit of the live text; every fix is a proposed edit against the live base.

## Go/No-Go (live context)

A live article can change while you work. Before the first step, and again before every applied change:

```bash
# 1. Fetch the current live state
curl -s "https://<edition>.wikipedia.org/w/index.php?title=<Title>&action=raw" -o /tmp/<title>-live-check.wikitext

# 2. Diff against the working-base snapshot
diff /tmp/<title>-live-fresh.wikitext /tmp/<title>-live-check.wikitext && echo "GO"
```

- `<Title>`: canonical title, spaces as underscores, special characters URL-encoded.
- **GO** (no output, exit 0): the live article is unchanged — safe to proceed.
- **Differences → NO-GO**: someone edited in the meantime. Stop, re-fetch a fresh base snapshot, re-check the affected findings against the new state. Never prepare or apply an edit on a stale base.

At session start, save the baseline: `/tmp/<title>-live-fresh.wikitext`. Reference it in the state file with a timestamp.

## File conventions

- Live snapshots and local working copies are **`.wikitext` files** — raw article source, never rendered text. Snapshot: `/tmp/<title>-live-*.wikitext`; working copy: `<title>.wikitext` in the working directory.
- Everything stays in wikitext: findings quote source lines, proposed diffs keep templates, categories, wikilinks, and citation markup intact. A fix that would break the markup is a defect.
- In draft context the same applies when the writer hands over a `.wikitext` file: audit and walkthrough work on the source, not on rendered prose.

## Step mechanics

One finding per step. Present exactly this, then wait:

```
[F2 · Major] Neutrality — unattributed evaluation
Current:  "KoliBri gilt als bahnbrechend für …"
Proposed: "Laut <Quelle> gilt KoliBri als …"
Reason:   evaluations belong to sources, not to the article (ground rule 1)
```

Writer's decision:

- **apply** — take the diff as proposed. Log it, move to the next finding.
- **change** — the writer adjusts the proposal (wording, scope, their own variant). Produce the new diff, discuss, decide. This loop is where targeted optimization happens: go as many rounds as the writer wants.
- **skip** — leave the passage untouched. Mark the finding *open*; it stays in the handover list.
- **stop** — pause the walkthrough. Record the position; the writer can resume in any later turn.
- **done** — close the walkthrough and hand over.

Rules:

- Show the diff, not a description of the diff. Quote the exact current passage and the exact replacement.
- One finding at a time. If the writer asks to jump to a specific finding (by ID), allow it, but keep every finding's decision explicit.
- When a decision invalidates later findings (e.g. a passage was cut entirely), say so at the affected step and mark them *obsolete* instead of walking through them.
- Blockers first, then Majors, then Minors/Polish — unless the writer steers otherwise.

## State file

Keep the walkthrough state in `WALKTHROUGH.md` in the working directory, so a session survives across turns:

```
Base: <draft file | live title + snapshot path + timestamp>
F1 [applied]     before → after, one-line reason
F2 [modified]    writer's variant applied — <what changed>
F3 [skipped]     open — <why>
F4 [open]        not yet discussed
```

Resume: read `WALKTHROUGH.md`, restate the base and progress in one line, continue at the first open finding. Re-run the Go/No-Go check first in live context.

## Handover (at `done`)

- The change log: every applied diff, before → after with its reason.
- The open findings, clearly flagged — they are work, not history.
- Live context: re-run the Go/No-Go check, then remind the writer in one line of the handover boundary (SKILL.md, Part B): they review every edit individually and transfer it themselves — the skill hands over prepared edits, never publishes.
- Draft context: route to re-`audit` if Blockers/Majors remain open, else offer `polish`.
