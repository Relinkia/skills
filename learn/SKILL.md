---
name: learn
description: Learn a subject in depth across conversations, keeping a map and one note per concept in Relinkia. Use for "explain", "capture", "new anchor", "where am I".
---

# Learn a subject with a Relinkia memory

Goal: turn conversations with Claude into cumulative knowledge. What gets understood in one conversation must not disappear with it. Works the same from claude.ai (web or mobile) and Claude Code, as long as the Relinkia MCP connector is active. Without Relinkia, see "Fallback mode" at the end.

## Setup (once per subject)
1. Ask for the subject and agree with the user on a dedicated scope, as a slug (e.g. `learn-rust`, `deep-learning`). Check with `list_scopes` that it doesn't exist yet.
2. Create the map: `create_note`, `type: "index"`, `docKey: "map"`, title "Map — <subject>", with sections: Method · Concepts seen (table) · Frontier · Anchors.

## Principle: descend from an anchor
- An **anchor** is a real question, article, post, chapter or paper.
- Descend one concept at a time: each concept is **called for** by a question raised by the previous one, never studied for its own sake.
- One concept at a time. If the user doesn't understand, rephrase differently (another angle, another example), not longer.

## Start of every session
1. `get_by_doc_key(scope, "map")` then `get_note_full`: know what has been seen, what is on the frontier, and what comes next.
2. If the requested concept already has a note (`get_by_doc_key(scope, <slug>)`), start from that note and from concepts already understood instead of starting over.

## Explanation format
- **Answer first**, in one or two sentences. No preamble.
- Start from the **real context** of the anchor, then generalize.
- A **worked concrete example** (with numbers when the subject allows), reused from one concept to the next when possible. Check every calculation.
- **Narrow ASCII diagrams** (≤ 36 characters wide) when the user is on mobile.
- **One analogy** from everyday life, well chosen.
- Always end with **"why here and not elsewhere"**: what problem the concept solves, why it is chosen, what breaks with the alternative.
- **Comparison** with neighboring concepts (table) and common **misconceptions**.
- A **practical example** when the subject allows (code, exercise, case).
- About two phone screens, unless asked to go deeper.
- Verify any recent or numeric fact with a web search, and cite the source.

## Capture (on "capture", or offered in one line at the end of a descent)

### One note per concept
`create_note`, `type: "synthesis"`, `docKey` = concept slug, readable title, `lastWriter` = surface (`claude-ai` or `claude-code`). If the note already exists: `get_note_full`, full enriched body, change summarized in one line, user confirmation, then `update_canonical` with `baseVersion`.

Template:
```
**Status**: understood | skimmed, on YYYY-MM-DD · anchor: [[Anchor — …]]
## Problem it solves
## Intuition
## Mechanism / content   (worked example)
## Why here
## Comparison
## Misconceptions
## Practice              (code, exercise or case)
## Recall test           (3 questions)
## Links                 (prerequisites · compare with · leads to · neighbors to study)
```
Link notes to each other with `[[Title]]`. Levels: **understood** (the user could re-explain and apply it) or **skimmed** (seen in context, to deepen later).

### One note per anchor
`type: "literature"`, `docKey: "anchor-<slug>"`, title "Anchor — …": source and link, key points, concepts uncovered, a critical take.

### Update the map
After each capture: add concepts seen (concept, level, date, anchor); remove from the **frontier** what was just studied; add to the frontier every concept spotted but not studied, with "← concept that raised it"; update anchors and the suggested next step.
Procedure: `get_note_full`, new full body, summary of the change, confirmation, `update_canonical` with `baseVersion`. On `CONFLICT_STALE_VERSION`: reread and ask again, never blindly increment the version.

## If Relinkia is unreachable
Lose nothing: write the planned notes and map changes to a temporary document (a claude.ai project document, or a local file in Claude Code) marked "PENDING". Once reconnected, on "capture", copy them into Relinkia, apply the map changes, then delete the temporary document.

## "Where am I" / choosing what's next
Summarize the map: number of concepts understood and skimmed, size of the frontier. Suggest **one** next step: the frontier concept that unlocks the most skimmed concepts, or the next anchor. Justify it in one sentence.

## Fallback mode (without Relinkia)
In Claude Code, use a folder of markdown files instead: `map.md` and one `<slug>.md` per concept, same templates, same rituals. Always reread a file in full before editing it. You lose versioning, conflict protection and cross-surface access, but keep the method.

## Avoid
- Explaining several concepts at once.
- Ending a descent without offering capture.
- Rebuilding a note from memory: always reread it in full with `get_note_full`.
