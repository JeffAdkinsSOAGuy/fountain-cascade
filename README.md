# Fountain Cascade

Fountain Cascade is an extension of the [Fountain](https://fountain.io) screenplay syntax. It adds story structure above and below the scene, and (in later versions) a way for co-writers, including AI, to propose alternatives without overwriting the writer's text.

**Status:** v0.2 draft. Expect changes.

## What it adds

Fountain describes a script as scenes made of lines (action, dialogue, and so on). A scene is a unit of place and time. Cascade adds the drama that runs through and across scenes:

| Layer | What it is | Version |
|---|---|---|
| Goal | What an agent wants, with a subject, an object, and a status that changes through the script | v0.2 |
| Sequence | A stretch of story that is a conflict between two goals or the creation of a goal | v0.1, redefined in v0.2 |
| Beat | A stretch in which the balance of power and the agents' objectives stay the same. Beats may cross scene headings. | v0.1, redefined in v0.2 |
| Stable IDs | On sequences, scenes, beats, and goals | v0.1 |
| Story spine | An ordered template of stages (e.g. the Hero's Journey) that parts of the script attach to | planned, v0.3 |
| Alternatives | Proposed replacement text beside the original, with an author | planned, v0.4 |

## Relationship to Fountain

Fountain 1.1, as published at [fountain.io](https://fountain.io/syntax), is the authority on Fountain syntax. Cascade does not redefine or replace any of it. Anything Cascade does not mention behaves exactly as Fountain defines it.

## The one rule

**Every Cascade file is a valid Fountain 1.1 file.**

Cascade keeps the `.fountain` extension and uses only constructs that existing Fountain tools already hide or ignore: sections, notes, boneyard comments, and title-page keys. A Cascade script opens, reads, and prints correctly in any Fountain tool. Those tools simply don't show the extra layers.

## Example

```
Title: Example
Structure: sequence

# The Dinner

[[id: q2]]

INT. DINING ROOM - NIGHT

[[id: s4]]

[[beat: A nice dinner]]

She pours him a second glass.

[[beat: She says it | ahead: WIFE]]

[[status: active | goal: divorce]]

[[goal: protect | id: reputation | subject: HUSBAND | object: his reputation]]

WIFE
I want a divorce.
```

Each Cascade note stands as its own paragraph, with a blank line above and below, so that Fountain's own rules for scene headings and dialogue are never disturbed.

See [SPEC.md](SPEC.md) for the full draft, [moral-dilemma.fountain](moral-dilemma.fountain) for a complete produced short film marked up with Cascade (currently with v0.1 markup: sequences and beats, no goals yet), and [ROADMAP.md](ROADMAP.md) for what comes next.

## Implementations

- FountainPen (editor, in development)

## License

The specification is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Anyone may implement it. See [LICENSE.md](LICENSE.md).

The example screenplay *Moral Dilemma* is not covered by that license. It is included for reference only, and all rights to it are reserved.

Fountain Cascade is an independent extension and is not affiliated with or endorsed by the authors of Fountain.
