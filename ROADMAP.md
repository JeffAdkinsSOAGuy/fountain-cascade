# Roadmap

This records what is planned after v0.3 and the design decisions already made, so they are not lost between versions. Nothing here is final until it appears in SPEC.md.

## v0.4: Alternatives

A way for a co-writer, human or AI, to propose replacement text without overwriting the original.

Decisions so far:

- **The live text is the current choice.** Alternatives sit beside it in boneyard comments, which other Fountain tools hide:

  ```
  [[alt: a7]]

  WIFE
  I want a divorce.

  /* alt: b | author: claude | why: she softens it and loses the upper hand
  WIFE
  I think we should talk about us.
  */

  [[end-alt: a7]]
  ```

- **An AI co-writer may only add alternatives.** It never changes live text.
- **Accepting swaps.** The chosen alternative becomes live and the previous original becomes an alternative.
- **Modifying creates a new alternative** under the writer's name. The proposed version is kept.
- **The smallest unit is one element:** a whole action paragraph or a whole dialogue block.
- **The script holds only pending alternatives.** Rejected ones move to a sidecar file (working name `script.fountain.rejected`), recording the alt ID, text, author, the original it was offered against, the date, and an optional reason.
- **The sidecar is optional.** Nothing in it is needed to read or print the script.

Undecided:

- Whether superseded originals also go to the sidecar, marked `superseded`.
- Whether the sidecar uses Fountain-style blocks or JSON.

## Later

- **More spines:** Save the Cat, three-act structure, and the Kenn Adams story spine, each described in goal terms like the Hero's Journey.
- **Setup and payoff:** connecting something planted in a preparation to the moment it pays off.
- **Want and need:** a place for what a character lacks without knowing it, beside the goals they pursue.
- **Sequence kinds:** whether a sequence records that it is a conflict, a preparation, or the creation of a goal.
- **Structural proposals:** suggesting a moved scene, a cut sequence, or a split beat. Alternatives cannot express these.
- **Tools:** FountainPen's beat agent reads a script and proposes goals, sequences, and beats. A plot view for planning with stages and goals before any script exists is next.

## Dropped

- **Threads.** Through-lines across non-adjacent scenes were planned as a separate layer. Goals that stay live across sequences (v0.2) cover this.
