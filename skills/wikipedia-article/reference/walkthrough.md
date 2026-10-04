# walkthrough — Step by step through the findings

Interactive companion to `audit` and `revise`. Instead of a batch fix run, you walk through the findings one at a time with the writer: show the diff, discuss it, sharpen it, then apply, change, or skip. Also the mode for preparing edits to a **live article** — with a Go/No-Go check before anything is transferred.

The conversation happens in the writer's language. You propose; the writer decides. Never apply ahead of a decision, never batch two steps into one.

## When

- After an audit, when the writer wants to discuss each fix individually instead of a batch `revise`.
- When the target is a live article and edits must be prepared against the current live state.

## Two contexts

- **Draft walkthrough** — base is the local draft file. Findings come from the audit (their stable IDs, F1, F2, …).
- **Live walkthrough** — base is the article's live wikitext. Findings come from an audit of the live text; every fix is a proposed edit against the live base.

## Two files, no more (live context)

Per article, exactly **two** `.wikitext` files in the working directory — never more, never versioned copies:

- **`<Title>.live.wikitext`** — the live mirror. The skill refreshes it itself:

  ```bash
  curl -s "https://<edition>.wikipedia.org/w/index.php?title=<Title>&action=raw" -o <Title>.live.wikitext
  ```

  This file is disposable and always regenerable; it never carries the writer's work.
- **`<Title>.wikitext`** — the working copy, the single place where edits are prepared. All decided diffs are applied here. This file carries the work; it is never overwritten automatically.

`<Title>`: canonical title, spaces as underscores, special characters URL-encoded in the URL. If the working copy does not exist yet, seed it from the live mirror.

Everything stays in wikitext: findings quote source lines, proposed diffs keep templates, categories, wikilinks, and citation markup intact. A fix that breaks the markup is a defect. In draft context the same applies when the writer hands over a `.wikitext` file: audit and walkthrough work on the source, not on rendered prose.

## Go/No-Go (live context)

The live article can change while you work. Before the first step, and again before every applied change, compare the fresh live state against the stored mirror — without creating extra files:

```bash
# GO if the stored mirror is still current:
diff <(curl -s "https://<edition>.wikipedia.org/w/index.php?title=<Title>&action=raw") <Title>.live.wikitext && echo "GO"
```

- **GO** (no diff output): safe to proceed.
- **NO-GO**: someone edited in the meantime. Re-sync the mirror in place (`curl … -o <Title>.live.wikitext`), then re-validate the walkthrough state against the new live text: open findings whose target passage changed get re-evaluated; decided-but-untransferred diffs are re-checked against the new state and reworked if they no longer apply cleanly. Never prepare an edit on a stale base.

## Step mechanics

One finding per step. Present exactly this, then wait:

```
[F2 · Major] Neutrality — unattributed evaluation
Current:  "KoliBri gilt als bahnbrechend für …"
Proposed: "Laut <Quelle> gilt KoliBri als …"
Reason:   evaluations belong to sources, not to the article (ground rule 1)
```

Writer's decision:

- **apply** — take the diff as proposed, into the working copy. Log it, move to the next finding.
- **change** — the writer adjusts the proposal (wording, scope, their own variant). Produce the new diff, discuss, decide. This loop is where targeted optimization happens: go as many rounds as the writer wants.
- **skip** — leave the passage untouched. Mark the finding *open*; it stays in the handover list.
- **stop** — pause the walkthrough. Record the position; the writer can resume in any later turn.
- **done** — close the walkthrough and hand over.

Rules:

- Show the diff, not a description of the diff. Quote the exact current passage and the exact replacement.
- One finding at a time. If the writer asks to jump to a specific finding (by ID), allow it, but keep every finding's decision explicit.
- When a decision invalidates later findings (e.g. a passage was cut entirely), say so at the affected step and mark them *obsolete* instead of walking through them.
- Blockers first, then Majors, then Minors/Polish — unless the writer steers otherwise.

## State file — resume or discard

Keep the walkthrough state in `WALKTHROUGH.md` in the working directory, so a session survives across turns:

```
Base: <Title>.wikitext — live mirror synced: <ISO timestamp>
F1 [applied]     before → after, one-line reason
F2 [modified]    writer's variant applied — <what changed>
F3 [skipped]     open — <why>
F4 [open]        not yet discussed
```

- **Resume** — any later turn, also a fresh session: read `WALKTHROUGH.md`, restate base and progress in one line, run the Go/No-Go check first in live context, continue at the first open finding.
- **Discard** — only on the writer's explicit request: delete `<Title>.wikitext` and `WALKTHROUGH.md`. The live mirror stays — it carries no work. Never discard on your own initiative; if the writer sounds unsure, ask once.

## Handover (at `done`)

- The change log: every applied diff, before → after with its reason.
- The open findings, clearly flagged — they are work, not history.
- Live context: re-run the Go/No-Go check, then remind the writer in one line of the handover boundary (SKILL.md, Part B): they review every edit individually and transfer it themselves — the skill hands over prepared edits, never publishes. Then ask once: keep the working copy for the transfer, or discard it.
- Draft context: route to re-`audit` if Blockers/Majors remain open, else offer `polish`.
