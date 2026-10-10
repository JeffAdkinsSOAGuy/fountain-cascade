# Fountain Cascade Specification

**Version:** 0.2 (draft)
**Date:** 2026-10-10
**Extends:** Fountain 1.1 (https://fountain.io/syntax)

The words MUST, SHOULD, and MAY are used as requirements on files and on tools that read or write them.

## 1. Relationship to Fountain

1.1. Fountain 1.1, as published at https://fountain.io/syntax, is the base of this specification and the sole authority on Fountain syntax.

1.2. Anything this specification does not mention behaves exactly as Fountain defines it.

1.3. Where this specification and Fountain disagree about a Fountain construct, Fountain is correct and this specification is in error.

1.4. This specification does not redefine, restrict, or replace any Fountain construct. It only assigns meaning to content that Fountain already permits.

1.5. Section 3 and Appendix A describe Fountain rules in this document's own words for the reader's convenience. They are informative. They are not a substitute for the Fountain specification.

## 2. Compatibility

2.1. A Cascade file MUST be a valid Fountain 1.1 file and uses the `.fountain` extension.

2.2. Cascade adds meaning only through constructs Fountain already defines: title-page keys, sections, synopses, notes, and boneyard comments.

2.3. Removing every Cascade note from a file MUST NOT change the printed screenplay.

2.4. A tool that does not understand a Cascade construct MUST preserve it unchanged when saving.

## 3. Fountain rules Cascade relies on (informative)

Cascade's placement rules exist because of these Fountain rules. See the Fountain specification for the authoritative wording.

- **Scene headings** need a blank line before and after them. A line placed directly under a scene heading can stop it being read as a heading.
- **Character cues** need a blank line before them and none after. A line placed directly above a cue can turn the whole dialogue block into action.
- **Forced elements** (`.` for a scene heading, `!` for action, `@` for a character) are recognised at the start of a paragraph. A line placed directly above one can stop the marker being recognised.
- **Notes** (`[[ ]]`) are hidden from the printed script and may stand alone or sit inside other text.
- **Sections** (`#`) and **synopses** (`=`) are hidden from the printed script and are used for outlining.
- **Boneyard** (`/* */`) content is ignored entirely.
- **Title-page keys** are `Key: value` lines at the top of the file, ending at the first blank line. Fountain permits keys beyond its standard ones.

## 4. Structured notes

Cascade carries most of its information in Fountain notes with a defined shape.

4.1. A structured note is a note whose content is one or more `key: value` fields separated by `|`:

```
[[key: value | key: value]]
```

4.2. The first key is the note's **type**. This specification defines the types `id`, `goal`, `status`, and `beat`.

4.3. Keys are lowercase letters, digits, and hyphens. Whitespace around keys, values, and `|` is ignored.

4.4. Within a field, only the first `:` separates the key from the value. Later colons are part of the value:

```
[[beat: The stakes: a dress with no corset under it]]
```

4.5. A literal `|` inside a value is written `\|`.

4.6. A note whose first key is not a type defined by this specification is an ordinary Fountain note and has no Cascade meaning.

4.7. A structured note MUST be a paragraph of its own: alone on its line, with a blank line before it and a blank line after it.

4.8. Rule 4.7 applies everywhere, including directly after a section line or scene heading and directly before a character cue.

## 5. The dramatic model

Cascade describes a script in two independent ways.

5.1. **The physical cut.** A scene is a unit of place and time, opened by a Fountain scene heading. Scenes exist for production. They carry no dramatic meaning in Cascade.

5.2. **The dramatic cut.** Sequences and beats are units of drama. They are defined by what agents want and who holds power, and they are free to cross scene headings.

5.3. An **agent** is anyone or anything that wants something and can act to get it. What it is does not matter: a person, a ghost, a machine, an animal, or a storm can be an agent if the story gives it a will. The writer decides.

5.4. A **goal** is something an agent wants to bring about over a stretch of story. A goal has a subject (the agent who wants it) and usually an object (the agent or thing it is aimed at). An agent may hold several goals at once, and one goal may serve another.

5.5. Every goal has a **status** at every point in the script. A goal may be `secret` (hidden from its object) or `active` (known to its object and being pursued). It ends as `won`, `lost`, or `abandoned`.

5.6. A **sequence** is a stretch of story about agents and their goals. It is either a conflict between two goals or the creation of a goal. A goal is not bound to one sequence: it may be created in one, stay secret through another, and be fought over in a third.

5.7. A **beat** is a stretch of a sequence in which the balance of power between the agents, and what each is trying to do at that moment, stay the same. A new beat begins where the power shifts or an agent's objective changes.

5.8. An **objective** is what an agent is trying to do right now in service of a goal. A **tactic** is how the agent goes about it. A change of tactic alone does not begin a beat. A tactic that succeeds does, because it shifts the power.

5.9. Without agents there is no drama. A passage with no agents, such as an establishing shot, belongs to no beat.

## 6. Structure levels

Fountain sections (`#`, `##`, ...) group scenes but carry no meaning. Cascade lets a script declare what each depth is.

6.1. The title-page key `Structure` lists level names from depth 1 downward, separated by commas:

```
Structure: act, sequence
```

Here `#` sections are acts and `##` sections are sequences.

6.2. The level names `act` and `sequence` are reserved. Other names MAY be used (for example `part` or `episode`).

6.3. Section depths beyond those listed have no Cascade meaning.

6.4. If `Structure` is absent, sections have no Cascade meaning.

## 7. Sequences

7.1. A sequence is a section at the depth named `sequence` in the `Structure` key. The text of the section line is the sequence's label.

7.2. A sequence runs from its section line up to the next section of the same or shallower depth.

7.3. A section line MUST have a blank line before and after it.

7.4. A synopsis (`=`) that follows the section line, with only blank lines and Cascade notes between them, is the sequence's summary. The synopsis MUST have a blank line before and after it.

## 8. Goals

8.1. A goal is declared by a structured note of type `goal`. The value is the want, written as a short verb phrase:

```
[[goal: be exclusive with | id: exclusive | subject: WIFE | object: GIRLFRIEND]]

[[goal: divorce | id: divorce | subject: WIFE | object: HUSBAND | for: exclusive | status: secret]]

[[goal: protect | id: reputation | subject: HUSBAND | object: his reputation]]
```

Each reads as a sentence: WIFE wants to divorce HUSBAND.

8.2. A goal note has these fields:

| Field | Required | Meaning |
|---|---|---|
| `id` | yes | The goal's ID (section 10). |
| `subject` | yes | The agent who holds the goal. Agents who share a goal are listed with commas. |
| `object` | no | The agent or thing the goal is aimed at. |
| `for` | no | The ID of another goal that this goal serves. |
| `status` | no | `secret` or `active`. If absent, the goal is `active`. |

8.3. An agent that appears as a character SHOULD be named as in its character cues, in capitals, so tools can match the goal to the character. Any other subject or object is free text.

8.4. A goal is declared once, at the point in the script where it is created. A goal note MAY appear anywhere in a sequence.

8.5. A goal is live from its declaration until it is won, lost, or abandoned. It is not ended by a scene heading or by the end of a sequence.

8.6. The `for` field records that one goal exists because of another. In 8.1, WIFE wants the divorce because she wants to be exclusive with GIRLFRIEND.

8.7. A change of status is recorded by a structured note of type `status`, placed at the point in the script where it happens. The value is the new status and the `goal` field names the goal:

```
[[beat: She says it]]

[[status: active | goal: divorce]]

[[goal: protect | id: reputation | subject: HUSBAND | object: his reputation]]
```

Here her secret goal comes into the open, and that creates his.

8.8. A `secret` goal is hidden from its object. Other agents, and the audience, may know of it. `secret` therefore applies only to a goal whose object is an agent.

8.9. The statuses are `secret`, `active`, `won`, `lost`, and `abandoned`. After `won`, `lost`, or `abandoned`, a goal is closed and MUST NOT change status again.

8.10. A status note MUST come after the declaration of the goal it names.

## 9. Beats

9.1. A beat is marked by a structured note of type `beat`. The value is a short description of the beat:

```
[[beat: He shuts her out so she can't say it]]

He runs into the house and locks the door.
```

9.2. A beat begins at its note. It ends at the next beat note or at the end of the sequence, whichever comes first. In a script with no sequences, it ends at the next beat note or the end of the file.

9.3. A scene heading does not end a beat. A beat MAY run through any number of scenes:

```
EXT. DRIVEWAY - DAY

[[beat: He shuts her out so she can't say it]]

He runs into the house and locks the door.

INT. HOUSE - CONTINUOUS

He runs to the bedroom. Locks the door.

EXT. DRIVEWAY - CONTINUOUS

[[beat: She gets through | ahead: WIFE]]

She puts in her key.
```

9.4. A beat begins between elements. It cannot begin inside an action paragraph or inside a dialogue block.

9.5. Content between the start of a sequence and its first beat note belongs to no beat.

9.6. Beats do not nest.

9.7. A beat note MAY carry an `ahead` field naming the agent who holds the upper hand during the beat.

## 10. Stable IDs

IDs let tools refer to a part of the script in a way that survives edits and reordering.

10.1. An ID is 1 to 32 characters from lowercase letters, digits, and hyphens.

10.2. An ID MUST be unique within the file. An ID that has been removed SHOULD NOT be reused.

10.3. A sequence or scene is given an ID by a structured note of type `id` in the first paragraph after its section line or scene heading:

```
## The Divorce

[[id: q7]]

[[goal: protect | id: reputation | subject: HUSBAND | object: his reputation]]

= She corners him at home and he runs out of places to hide.

EXT. DRIVEWAY - DAY

[[id: s31]]
```

10.4. A beat or goal is given an ID by an `id` field in its own note.

10.5. IDs on sequences, scenes, and beats are optional in hand-written files. A goal MUST have an ID, because status notes and other goals refer to it. A goal's ID MAY be a plain word, such as `divorce`. A tool that needs an ID for an element that has none SHOULD assign one and write it to the file.

10.6. IDs are not scene numbers. Fountain scene numbers (`#12#`) remain display numbers and MAY change between drafts. IDs do not change.

## 11. Changes from v0.1

11.1. In v0.1 a beat ended at the next scene heading. From v0.2 it does not (9.2, 9.3). A v0.1 file read under v0.2 has the same beats, but each may now extend past the end of its scene.

11.2. In v0.1 a beat was undefined. Section 5 now defines it.

## 12. Open questions

These are undecided and feedback is welcome.

- **Sequence kinds.** Whether a sequence should record that it is a conflict or the creation of a goal, or whether tools should work that out from its goals.
- **Goals that begin before the script does.** A goal is declared where it is created (8.4), but some are already held when the story opens. The example declares such a goal where its holder first comes into play.
- **Which goal a beat belongs to.** When an agent holds several goals, a beat does not say which one is in play.
- **Beats that turn mid-element.** A turn that happens halfway through a speech or paragraph can only be marked at the next element (9.4).
- **Layers.** Beats form a single line through a sequence and cannot say that a beat belongs to a frame story or a second point of view.
- **Partly marked files.** The last marked sequence runs to the end of the file or the next section. There is no way to end a sequence early.
- **Scene IDs.** Whether scene IDs should reuse Fountain's scene-number syntax instead of a separate note.

## Appendix A. Fountain quick reference (informative)

This is a summary in this document's own words so that Cascade can be read on its own. It is not the Fountain specification and omits detail. If it differs from https://fountain.io/syntax, Fountain is correct.

| Element | How Fountain recognises it | Force with |
|---|---|---|
| Title page | `Key: value` lines at the top of the file, ending at the first blank line. Indented lines continue a value. | |
| Scene heading | A line starting `INT`, `EXT`, `EST`, `INT./EXT`, `INT/EXT`, or `I/E`, with a blank line before and after. | Leading `.` |
| Action | Any paragraph not recognised as something else. | Leading `!` |
| Character | A line in all capitals with a blank line before it and none after. | Leading `@` |
| Dialogue | The text following a character or parenthetical. | |
| Parenthetical | A line in `( )` inside a dialogue block. | |
| Dual dialogue | A `^` after the second character's name. | |
| Lyrics | A line starting `~`. | |
| Transition | A line in all capitals ending `TO:`, with a blank line before and after. | Leading `>` |
| Centered text | `> text <` | |
| Emphasis | `*italic*`, `**bold**`, `***bold italic***`, `_underline_` | |
| Page break | A line of three or more `=`. | |
| Scene number | `#number#` at the end of a scene heading. | |
| Note | `[[text]]` | |
| Boneyard | `/* text */` | |
| Section | A line starting with one or more `#`. | |
| Synopsis | A line starting with a single `=`. | |
