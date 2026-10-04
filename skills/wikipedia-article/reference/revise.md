# revise — Apply findings, coached

Applies audit findings to a draft, under Mentor rules. Read `STYLE.md` if present.

## Order

Fix in severity order: Blockers, then Majors, then Minors, then Polish. Do not beautify a sentence whose paragraph still lacks a source.

## Per finding

1. Restate the rule behind the finding in one line — the writer must understand the rule, not just receive the fix. Cite the policy by name (NPOV, Verifiability, No original research, BLP, …).
2. Fix the draft.
3. Record: **resolved** (with what changed) or **open** (with what is missing and who must provide it — usually a better source).

## Pushback

When the writer disagrees, explain the reasoning with an example — but the policies win. Offer the closest rule-compliant alternative; do not trade away the rule itself.

## Patterns

Track violation types across revision rounds. The same failure three times is a pattern: address the pattern explicitly (e.g. "unattributed evaluations keep appearing — rule: every evaluation gets 'according to <source>'").

## Output

End with a finding table:

```
| # | Severity | Finding | Status | Change |
```

Then recommend a fresh `audit`. A revised draft is unproven until the Advocate has seen it again.

Also derive from the table a **suggested edit summary** for the later transfer to Wikipedia (same format as `walkthrough`, handover): one line, content-focused, grouped by change type.
