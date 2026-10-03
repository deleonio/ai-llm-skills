# assess — Notability gate and source map

Run before anything is written. Output only the assessment — no article prose in this mode.

## 1. Search

Search for independent, reliable, secondary sources on the topic. Cover multiple angles: press, specialized literature, academic work, reference works. Search in the target edition's language first, then others.

## 2. Judge each source

For every candidate:

- **Independence** — who is speaking: the subject, or others? Press releases, own website, interviews about their own work fail.
- **Reliability** — editorially reviewed? Known publisher? Corrections policy? Blogs, forums, social media, wikis fail.
- **Depth** — significant coverage (a substantial passage or more devoted to the subject) or a trivial mention (a name in a list, a one-line brief)?

## 3. Verdict on notability

Per the edition's notability guideline:

- **Notable** — 2–3+ sources that are independent, reliable, secondary, with significant coverage. List them.
- **Borderline** — name exactly what evidence is missing and what would close the gap.
- **Not notable** — say so plainly, without softening. State what would change the verdict.

## Output

A source table:

```
| Source | Type | Independent | Reliable | Depth | Counts? |
```

Then the verdict with the sources that carry it. If the verdict is *not notable*, this ends the pipeline — do not draft anyway.

Not counted regardless of quality: press releases, routine news briefs, databases and listings, primary data, the subject's own publications.
