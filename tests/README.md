# Conformance cases

Small files for checking a tool against the Fountain Cascade specification. There are two kinds, because there are two different jobs.

## `format`: does a tool read a file correctly?

Each case is a `.fountain` file and a `.json` file of the same name. The JSON is what the file means under the specification. A tool that reads Cascade should arrive at the same thing.

| Field | Meaning |
|---|---|
| `structure` | The level names from the `Structure` key. |
| `spines` | The spines the file names. A custom spine is given as its stage IDs. |
| `outline` | Everything in the file in order: sections (with what they contain), scenes, beats, goal declarations, and status changes. A beat's `scenes` is the number of scenes it runs through. |
| `goals` | Each goal, with the statuses it passes through in order. |
| `problems` | The line numbers a tool should report a problem on. The wording of a report is up to the tool. |

A field that does not apply is left out. Several cases contain deliberate mistakes: the specification says what a file means, and these pin down which lines a tool should question and what it should still make of the rest.

## `analysis`: does a tool find the drama a reader would?

Each case is a short unmarked excerpt, `name.fountain`, and the same excerpt with the marks a careful reader would add, `name.expected.fountain`. They are for tools that propose marks, such as an AI assistant.

Analysis is a judgment, so the comparison is not word for word. What should match is stated per case:

| Case | What should match |
|---|---|
| `01-beat-through-scenes` | Two beats, not four. The second starts when he runs and carries through both later scene headings. |
| `02-tactic-is-not-a-beat` | No beat when she shouts or when he sings louder: those are tactics. One beat where the lipstick works. |
| `03-secret-until-its-object-knows` | The divorce goal is declared in the first scene as secret, although the audience now knows it. It becomes active only at the line where she tells her husband. |
| `04-a-goal-is-raised` | A new goal with `from: use-tom` and no `for`. The goal it grew out of is not marked abandoned. |
| `05-pause-and-resume` | Two sequences and one resume. The third stretch is not a third sequence. |

Wording of beats, titles, and reasons, the choice of IDs, and the `ahead` field are not compared.

The excerpts were written for this purpose and are covered by the same license as the specification.
