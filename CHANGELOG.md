# Changelog

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
