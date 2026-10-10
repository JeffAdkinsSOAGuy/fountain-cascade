# Changelog

## v0.3.1-draft (2026-10-10)

Tightening after an outside review of v0.3.

- Added: the allowed status changes, as a table. A goal in the open cannot become secret again, and a status note must change the status.
- Clarified: a beat ends where its sequence pauses, and a resumed stretch needs a beat of its own.
- Added: a sequence in which agents are present should open with a beat.
- Added: conformance cases in `tests`. Eleven `format` cases pair a file with what it means, including which lines are in error. Five `analysis` cases pair an unmarked excerpt with the marks a careful reader would add.
- Fixed: in `moral-dilemma.fountain`, Suzie's goal of cashing in Nana was marked won when she agreed. She never collects, so it is now marked lost when she is taken away.

## v0.3-draft (2026-10-10)

Story arcs, and a goal model deep enough to plan a plot before writing it.

- Added: spines and stages. The `Spine` title-page key names a story arc, and `stage` attaches one of its stages to a sequence or a beat. A script may define a custom spine.
- Added: the first library spine, the Hero's Journey, with each stage described in terms of goals.
- Added: `resume`, so a sequence can pause while another plays and then continue.
- Added: the goal tree. `for` names the goal a goal serves; a goal with none is top-level.
- Added: `from`, for a goal raised out of another, or replacing an abandoned one.
- Added: a plot may be written with no script text.
- Clarified: agents may enter or leave during a sequence; a sequence often, but not always, ends when its goal is won or lost.
- Updated: `moral-dilemma.fountain` pauses one sequence for another and resumes it, and links its goals into a tree.
- Every v0.2 file is a valid v0.3 file with the same meaning.

## v0.2-draft (2026-10-10)

Sequences and beats are now defined by drama, not by scene headings.

- Added: the dramatic model. Scenes are physical units; sequences and beats are dramatic units.
- Added: definitions of agent, goal, status, sequence, beat, objective, and tactic.
- Added: `goal` notes with `subject`, `object`, `for`, and `status`.
- Added: `status` notes. A goal is `secret` (hidden from its object) or `active`, and ends `won`, `lost`, or `abandoned`.
- Changed: a beat runs until the next beat or the end of the sequence. A scene heading no longer ends a beat.
- Added: the optional `ahead` field on beats.
- Changed: a sequence is a conflict between two goals or the creation of a goal.
- Updated: `moral-dilemma.fountain` is re-marked under v0.2, with 8 goals and 22 beats in 5 sequences. Sequence q2 and 25 beat IDs from the v0.1 markup are retired, not reused.

## v0.1.1-draft (2026-10-10)

Changes from testing v0.1 against a full-length screenplay.

- Fixed: structured notes must be paragraphs of their own, with a blank line before and after. The v0.1 placement (directly under a scene heading or directly above the text) broke scene headings and dialogue in a standard Fountain parser.
- Added: only the first colon in a field separates key from value.
- Added: Fountain 1.1 named as the sole authority on Fountain syntax.
- Added: an informative section on the Fountain rules Cascade relies on, and an informative Fountain quick reference.
- Added: beats begin between elements.
- Replaced the invented sample with `moral-dilemma.fountain`, a produced short film marked up in full.
- Updated: the README example.
- License: the example screenplay is excluded from CC BY 4.0.
- Open questions extended with the gaps the test exposed.

## v0.1-draft (2026-10-10)

First public draft.

- Structured notes
- `Structure` title-page key
- Sequences
- Beats
- Stable IDs
