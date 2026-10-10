# Fountain Cascade Specification

**Version:** 0.1 (draft)
**Date:** 2026-10-10
**Extends:** Fountain 1.1 (https://fountain.io/syntax)

The words MUST, SHOULD, and MAY are used as requirements on files and on tools that read or write them.

## 1. Compatibility

1.1. A Cascade file MUST be a valid Fountain 1.1 file and uses the `.fountain` extension.

1.2. Cascade adds meaning only through constructs Fountain already defines: title-page keys, sections, synopses, notes, and boneyard comments.

1.3. Removing every Cascade note from a file MUST NOT change the printed screenplay.

1.4. A tool that does not understand a Cascade construct MUST preserve it unchanged when saving.

## 2. Structured notes

Cascade carries most of its information in Fountain notes with a defined shape.

2.1. A structured note is a note whose content is one or more `key: value` fields separated by `|`:

```
[[key: value | key: value]]
```

2.2. The first key is the note's **type** (for example `beat` or `id`).

2.3. Keys are lowercase letters, digits, and hyphens. Whitespace around keys, values, and `|` is ignored.

2.4. A literal `|` inside a value is written `\|`.

2.5. A note whose first key is not a type defined by this specification is an ordinary Fountain note and has no Cascade meaning.

2.6. A structured note MUST be on a line of its own.

## 3. Structure levels

Fountain sections (`#`, `##`, ...) group scenes but carry no meaning. Cascade lets a script declare what each depth is.

3.1. The title-page key `Structure` lists level names from depth 1 downward, separated by commas:

```
Structure: act, sequence
```

Here `#` sections are acts and `##` sections are sequences.

3.2. The level names `act` and `sequence` are reserved with their usual screenwriting meaning. Other names MAY be used (for example `part` or `episode`).

3.3. Section depths beyond those listed have no Cascade meaning.

3.4. If `Structure` is absent, sections have no Cascade meaning.

## 4. Sequences

4.1. A sequence is a section at the depth named `sequence` in the `Structure` key.

4.2. A sequence contains every scene from its section line up to the next section of the same or shallower depth.

4.3. A synopsis line (`=`) directly after the section line is the sequence's summary.

```
## The Arrival
= Mara returns home and finds the house sold.
```

## 5. Beats

A beat is a unit of story inside a scene.

5.1. A beat is marked by a structured note of type `beat`. The value is a short description of the beat:

```
[[beat: Mara pretends she already knew]]
```

5.2. A beat begins at its note and ends at the next beat note, scene heading, or section, whichever comes first.

5.3. Content between a scene heading and the scene's first beat note belongs to the scene but to no beat.

5.4. Beats do not nest.

5.5. A scene MAY have no beats.

## 6. Stable IDs

IDs let tools refer to a part of the script in a way that survives edits and reordering. Later versions of this specification depend on them.

6.1. An ID is 1 to 32 characters from lowercase letters, digits, and hyphens.

6.2. An ID MUST be unique within the file. An ID that has been removed SHOULD NOT be reused.

6.3. A sequence or scene is given an ID by a structured note of type `id` on the line directly after its section line or scene heading. If a sequence also has a synopsis, the `id` note comes before it:

```
## The Arrival
[[id: q1]]
= Mara returns home and finds the house sold.

INT. KITCHEN - DAY
[[id: s1]]
```

6.4. A beat is given an ID by an `id` field in its beat note:

```
[[beat: Mara pretends she already knew | id: b1]]
```

6.5. IDs are optional in hand-written files. A tool that needs an ID for an element that has none SHOULD assign one and write it to the file.

6.6. IDs are not scene numbers. Fountain scene numbers (`#12#`) remain display numbers and MAY change between drafts. IDs do not change.

## 7. Open questions

These are undecided in v0.1 and feedback is welcome.

- **ID placement.** Whether scene IDs should reuse Fountain's scene-number syntax instead of a separate note. The draft keeps them separate because production scene numbers get renumbered.
- **Beat descriptions.** Whether the description in a beat note is required or may be empty.
- **Levels below sequence.** Whether `Structure` should be able to name the scene and beat levels too, for scripts that use different terms.
