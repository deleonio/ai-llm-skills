# sources — Find and verify usable sources

For a topic or a list of claims, find and verify sources. Only sources that exist and were actually checked go into the output.

## Hard rule

**Never invent a source.** No fabricated authors, titles, years, URLs, DOIs, ISBNs. A hallucinated citation is worse than a missing one. If a web search or fetch tool is available, verify every source before listing it: does it exist, is it accessible, and does it say what it is claimed to say? If you cannot verify, say so — do not guess.

## Per claim

1. Search for the best available support: specialized literature, quality press, academic journals, reference works first.
2. Rank candidates: independence, reliability, depth of coverage.
3. Pick the best 1–3. Reject the rest with a reason.

## Output

```
Claim: <the claim, quoted>
Supported by:
  [1] <full citation> — says: <one-line summary of the supporting passage>
  [2] …
Rejected: <candidate> — <reason: press release / primary only / blog / trivial mention / non-independent>
Uncovered: <claims with no usable source — flagged, never papered over>
```

Claims that stay uncovered are a finding for the audit, not a problem to hide: either the claim goes or better sources must be found.

## Ranking hints

- Press releases and company pages may confirm *that* something is claimed, never *that* it is true.
- A source can be reliable and still non-independent for the subject (trade press interview with the founder).
- Primary sources (laws, studies, financial reports) support bare facts; interpretation must come from secondary sources.
