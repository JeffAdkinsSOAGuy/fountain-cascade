# Fountain Cascade Specification

**Version:** 0.1.1 (draft)
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

4.2. The first key is the note's **type** (for example `beat` or `id`).

4.3. Keys are lowercase letters, digits, and hyphens. Whitespace around keys, values, and `|` is ignored.

4.4. Within a field, only the first `:` separates the key from the value. Later colons are part of the value:

```
[[beat: The stakes: a dress with no corset under it]]
```

4.5. A literal `|` inside a value is written `\|`.

4.6. A note whose first key is not a type defined by this specification is an ordinary Fountain note and has no Cascade meaning.

4.7. A structured note MUST be a paragraph of its own: alone on its line, with a blank line before it and a blank line after it.

4.8. Rule 4.7 applies everywhere, including directly after a section line or scene heading and directly before a character cue.

## 5. Structure levels

Fountain sections (`#`, `##`, ...) group scenes but carry no meaning. Cascade lets a script declare what each depth is.

5.1. The title-page key `Structure` lists level names from depth 1 downward, separated by commas:

```
Structure: act, sequence
```

Here `#` sections are acts and `##` sections are sequences.

5.2. The level names `act` and `sequence` are reserved with their usual screenwriting meaning. Other names MAY be used (for example `part` or `episode`).

5.3. Section depths beyond those listed have no Cascade meaning.

5.4. If `Structure` is absent, sections have no Cascade meaning.

## 6. Sequences

6.1. A sequence is a section at the depth named `sequence` in the `Structure` key.

6.2. A sequence contains every scene from its section line up to the next section of the same or shallower depth.

6.3. A section line MUST have a blank line before and after it.

6.4. A synopsis (`=`) that follows the section line, with only blank lines and an `id` note between them, is the sequence's summary. The synopsis MUST have a blank line before and after it.

```
## The Arrival

= Mara returns home and finds the house sold.

```

## 7. Beats

A beat is a unit of story inside a scene.

7.1. A beat is marked by a structured note of type `beat`. The value is a short description of the beat:

```
[[beat: Mara pretends she already knew]]

Mara sets down her bag. Smiles too quickly.
```

7.2. A beat begins at its note and ends at the next beat note, scene heading, or section, whichever comes first.

7.3. A beat begins between elements. It cannot begin inside an action paragraph or inside a dialogue block.

7.4. Content between a scene heading and the scene's first beat note belongs to the scene but to no beat.

7.5. Beats do not nest.

7.6. A scene MAY have no beats.

## 8. Stable IDs

IDs let tools refer to a part of the script in a way that survives edits and reordering. Later versions of this specification depend on them.

8.1. An ID is 1 to 32 characters from lowercase letters, digits, and hyphens.

8.2. An ID MUST be unique within the file. An ID that has been removed SHOULD NOT be reused.

8.3. A sequence or scene is given an ID by a structured note of type `id` in the first paragraph after its section line or scene heading. For a sequence with a synopsis, the `id` note comes before the synopsis:

```
## The Arrival

[[id: q1]]

= Mara returns home and finds the house sold.

INT. KITCHEN - DAY

[[id: s1]]

Boxes everywhere.
```

8.4. A beat is given an ID by an `id` field in its beat note:

```
[[beat: Mara pretends she already knew | id: b1]]
```

8.5. IDs are optional in hand-written files. A tool that needs an ID for an element that has none SHOULD assign one and write it to the file.

8.6. IDs are not scene numbers. Fountain scene numbers (`#12#`) remain display numbers and MAY change between drafts. IDs do not change.

## 9. Open questions

These are undecided and feedback is welcome.

- **What counts as a beat.** The specification does not define one, so two people marking the same scene will disagree on the count.
- **Beats that turn mid-element.** A turn that happens halfway through a speech or paragraph can only be marked at the next element (7.3).
- **Scenes that change location without a heading.** Cascade treats one scene heading as one scene.
- **Units between sequence and scene.** Montages and intercuts contain several scene headings but act as one unit. There is no level for them.
- **Layers within a scene.** Beats form a single line through a scene and cannot say that a beat belongs to a frame story or a second point of view.
- **Partly marked files.** The last marked sequence runs to the end of the file or the next section. There is no way to end a sequence early.
- **ID placement.** Whether scene IDs should reuse Fountain's scene-number syntax instead of a separate note.
- **Levels below sequence.** Whether `Structure` should be able to name the scene and beat levels too.

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
