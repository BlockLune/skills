# English Technical Writing & Anti-Slop

## Reader-focused sentences (Google developer style)

- Address the reader as "you" in the present tense. Reserve "will" for events that genuinely happen later.
- Name the actor: write "the compiler checks", not "is checked". Use passive voice only when the actor is unknown or irrelevant.
- Write instructions as imperative commands: "Click Submit." Put the condition or warning before the instruction: "To delete the document, click Delete." Put the common case first and exceptions after.
- Use short, everyday words: "use" (not "utilize"), "help" (not "facilitate"), "do" (not "perform"), "to" (not "in order to"). Cut "please", "simply", "easy", and "quickly" from procedures.
- Write the real symbol, file, flag, or command name from the codebase. Replace invented metaphors ("evacuate", "ratchet", "endgame") with plain words ("move", "delete", "a budget that only decreases").
- Use sentence case for headings. Write task headings as bare verb phrases ("Create an instance") and concept headings as noun phrases.
- Format code in `code font`. Use bold and italics sparingly: convey emphasis and structure through sentence order, paragraph breaks, and punctuation rather than habitual Markdown markers. Use serial commas. Drop "etc." and state up front when a list is partial.

## Single-load statements (STE rules)

- Keep one instruction per sentence (under ~20 words) and one thought per sentence elsewhere (under ~25 words).
- Keep articles ("the", "a"): "Remove the backup file" has one reading; "Remove backup file" has two.
- Give each word one meaning and stick to one verb per action ("start" everywhere, not "start" and "initiate").

## Unambiguous syntax (Global English)

- Place modifiers like "only" and "not" directly next to the word they modify ("fails only on growth", not "only fails on growth").
- Break up noun strings longer than three words: change "the proto import budget check script" to "the script that checks the proto-import budget".
- Make every "it", "they", and "this" point to one obvious noun. Repeat the noun when in doubt; never use "this" or "which" to refer to an entire clause.
- Keep verbs in parallel clauses ("Phase 1 moves the converters and Phase 2 moves the runtime") and structural words like "that" ("Ensure that the switch is off").
- Repeat articles in a series when needed to prevent misreading ("the client and the host"). Disambiguate groupings with "both...and", "either...or", or "if...then".
- Use periods instead of semicolons (`;`) or em dashes (`—`). Make parenthetical text a complete grammatical unit or a separate sentence.
- Write "a, b, or both" instead of "a/b" or "and/or". Avoid forming plurals with "(s)". Skip idioms, colloquialisms, and Latin abbreviations (`e.g.`, `i.e.`).

## Anti-slop patterns

- Cut rhetorical contrasts (`It's not just X; it's Y`, `Not because X. Because Y.`) unless correcting a genuine technical misconception.
- Cut throat-clearing and sign-offs (`Here's the thing:`, `Let's dive in`, `It is important to note that`, `That is the real win.`, `Let that sink in.`).
- Cut trailing participial hype (`, highlighting / underscoring / showcasing...`); use `to <verb>` or a separate sentence stating the concrete effect.

## Examples

| Before | After |
| --- | --- |
| In this section, we'll discuss auth. It's worth noting that the table below compares three options. | Use Option A (short-lived JWT + refresh token). |
| The new retry policy — introduced after last week's outage — batches writes every 50 ms; it also caps backoff at 30 s, underscoring scalable design. | The retry policy batches writes every 50 ms to reduce disk I/O and caps backoff at 30 s. We added this policy after last week's outage. |
| Configuration of the proto import ratchet budget script parameters is performed via budget.json. Note that it's important to remember that running with --write, which updates the committed budget to reflect the current count, should only be done when lowering it. If exceeded, CI fails. | `budget.mjs` reads the committed budget from `budget.json` and counts the files that import protos. If the count exceeds the budget, CI fails. Run `budget.mjs --write` only to lower the budget. |
