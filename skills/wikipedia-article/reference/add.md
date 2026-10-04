# add — Add new content, information, or an event

Adds one new piece of content to an article — a new fact, new information, a new event — under full mentor guard. Works on a local draft or, via the two-files rule (`walkthrough`), on a live article. Adding is not free: every gate that guards a whole article guards a single addition too.

## 1. Intake

What exactly is new? One sentence from the writer is enough. Restate it as the claim to be added; ask once if it is ambiguous.

## 2. Weight gate (before anything else)

Not everything that happened belongs in the article:

- Weight follows long-term significance (ground rule 6). A single press item does not earn a passage, let alone a section.
- Routine coverage — product-launch briefs, match results, routine personnel changes, anniversary pieces — is rejected with a reason.
- The addition needs significant coverage in independent, reliable, secondary sources, exactly like notability for a whole article.
- On rejection: say it openly, in one line, and what would change the verdict. A rejected addition is never smuggled into the lead or the infobox instead.

## 3. Sources

Run the `sources` rules for the new claim: best available support first, human reads every source before it becomes a citation. No verified sources → stop; the addition waits until there are some.

## 4. Placement

- Existing section first. A new section only when the content genuinely establishes one — and only if it will still matter long-term.
- Chronology for people, aspect-based placement for topics.
- Lead only when the addition changes the overall picture of the subject — and then the lead is updated to summarize the body, never to host the news item itself.
- Check the surrounding text: does the addition contradict, duplicate, or date other passages? Those get fixed in the same pass, as their own diffs.

## 5. Draft under guard

Write the passage under the ground rules: attributed, neutral, cited at the sentence for load-bearing claims. Machine-tell rules apply from the first sentence.

- **Live context:** the diff goes into the working copy (`<Title>.wikitext`), discussed step by step per `walkthrough` step mechanics — the writer can change or skip. Wikitext markup stays intact. Run the Go/No-Go check before the diff is applied.
- **Draft context:** the passage is added to the draft, marked as new so the next audit sees it.

## 6. Handover

- The change log: the new passage, plus any surrounding passages fixed in the placement pass.
- A suggested edit summary (handover format): e.g. "Rezeptionsabschnitt um <Ereignis> ergänzt (Quellen: …)".
- Open questions — especially anything the writer must still verify themselves (Part B boundary).
- Live context: the skill itself runs the Go/No-Go check at handover and states the verdict — "GO as of now" or "NO-GO, re-sync first" (then re-validate before handing over again). The check is momentary; the writer can request a fresh one right before transferring. The writer reviews and transfers every edit themselves.
- Draft context: recommend a fresh `audit` — a new passage is unproven until the Advocate has seen it.
