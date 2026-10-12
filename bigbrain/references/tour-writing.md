# Writing the tour

The page is read, not studied: every sentence must save the reviewer more time than it costs.

## Summary

The page opens on `summary`: why the PR exists and what it does, in 10 lines at most. Someone who reads only this knows the problem, what changes, for whom, how, and how it is tested.

```markdown
**One or two sentences for someone who does not know the code: the problem the PR solves, and what it does about it, seen from the user or the product.**

A short paragraph on how things worked until now and how they work after this PR, now in the code's terms.

- A full sentence on the main mechanism.
- Another on a second piece, if there is one.
- Another on a decision worth knowing, and its reason.

A sentence on how the change is tested, and what no test covers.
```

No heading, no paragraph over two lines.

The opening names no file, function, or field: it speaks of screens, features, and users. Take the problem from the description, the linked issue, or the commits. When none of them states one, say what the PR changes for the user and write that the description gives no reason, rather than inventing one.

When the PR changes what a user sees or reads (a message, a label, a screen), quote it before and after, as is, in the summary or the first step, in a `>` quote. The reviewer judges the result before the mechanism.

## Tone

Write the way a colleague explains the PR out loud: full sentences, each with a subject and a verb, linked by ordinary words ("jusqu'ici", "donc", "mais"). Short does not mean telegraphic. Never write notes ("Before, one button. Now, two cards."), fragments as bullets, or clauses stacked with semicolons.

## Where each thing goes

Each fact goes to the narrowest place that can hold it, and only there.

| Place | Holds |
|---|---|
| Step `body` | What this part does in the flow, how, and why when a decision was made. |
| Panel `note` | What this file is in the flow, in one sentence. |
| `highlights` | What specific lines do, or a demonstration on them: the condition that decides, the line that could break, the assertion that proves it. |
| Badge `[[path:lines]]` | Code worth a look outside the panels: a caller, the previous version, a related test. |
| `checks` | A doubt the reviewer must settle to accept the step. |

A highlight never repeats the body, and a check never restates a highlight or the body.

## Explaining a step

- **Body: role, mechanism, decision.** First what this part does in the flow, for the user or the caller. Then how it works. Then a decision as "X rather than Y because Z" when there is one. 2 to 4 sentences, under about 90 words. Do not narrate the diff.
- **Three code names at most in a body.** Each name is one more thing the reader holds in mind. Say the rest in words ("the function that rebuilds the sentence") or move it to a highlight, and write a name whole, never cut short with "…".
- **Highlights carry the detail.** 1 to 3 per panel, only on the lines the step hinges on, each opening a note of one or two sentences that explains or demonstrates ("A cancelled navigation still resolves, with a failure: this branch keeps the message from being sent."). This is what the raw diff lacks. A panel shown for context may have none.
- **One or two checks.** The question the reviewer must settle to accept the step, most often how it could break or what the diff leaves out, pointing at lines. Prefer a finding with a failure scenario over a hunch. A step rated `low` may have none.
- **Ask whether it is needed.** When the PR adds a layer or puts the same rule in two places (a server prompt and client code, a copied helper), one check asks whether both are needed and names the simpler alternative.
- **Tests sit with what they test.** Show a test in the step whose behavior it checks, as a panel or a badge, not in a last step of its own that the reader reaches tired. A step whose check points at missing coverage is not rated `low`.

## Rules

- **Plain language** for a competent engineer new to this area. Define a new name where the reader first meets it.
- **Read long lines word by word.** A changed line over about 160 characters (a prompt, a message, a config string) shows as removed and re-added whole. Before saying what it adds or drops, read it in `diff.words.patch`; `overview.md` flags those hunks.
- **Anchor every fact** in lines with badges or highlights, never pasted code. A claim about tests ("covered by…") names the test. Word an inference as one ("probably"), and what you could not check in the first person ("I found no caller that…").
- **No decoration.** No alert blocks, no emoji, no headings inside a body, no bold beyond one key phrase.
- **Don't reassure.** Avoid "simply", "correctly", "safely", "trivial": judging is the reviewer's job, and `build` warns on these words. Give no overall verdict.
