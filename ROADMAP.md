# Roadmap

This records what is planned after v0.2 and the design decisions already made, so they are not lost between versions. Nothing here is final until it appears in SPEC.md.

## v0.3: Story spines

A spine is a named, ordered list of stages that parts of a script attach to. The Hero's Journey is one example.

Decisions so far:

- **Spine definitions live outside the script.** This repository will carry a small library of standard spines (Hero's Journey, Save the Cat, three-act, the Kenn Adams story spine).
- **A script names its spine in the title page:** `Spine: heros-journey`.
- **A custom spine is defined in the title page** using indented multi-line values:

  ```
  Spine: custom
      setup: The Marriage She Performs
      rupture: Not Until You're Divorced
  ```

- **Stages attach by structured note** at the sequence, scene, or beat level: `[[stage: ordinary-world]]`, or as a field in a beat note: `[[beat: The letter arrives | stage: call-to-adventure]]`.
- **Stages attach to units; they do not run until the next marker.** This allows overlap and out-of-order stages.
- **Each stage has** an ID, a display name, and optionally a description and an expected position in the script.

Undecided:

- Whether a script may use more than one spine, with stages written `[[stage: heros-journey/ordeal]]`.

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

- **Structural proposals:** suggesting a moved scene, a cut sequence, or a split beat. Alternatives cannot express these.
- **An AI beat agent:** a tool that reads a whole script, works out its agents, goals, and shifts of power, and proposes sequences and beats for the writer to accept or reject. Being built in FountainPen.

## Dropped

- **Threads.** Through-lines across non-adjacent scenes were planned as a separate layer. Goals that stay live across sequences (v0.2) cover this.
