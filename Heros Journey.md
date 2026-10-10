# The Hero's Journey

**Spine ID:** `heros-journey`

Twelve stages, in the form popularised for screenwriters by Christopher Vogler from Joseph Campbell's work. The stage names are the commonly used ones. The descriptions are this repository's own, and say what each stage usually looks like in Cascade's terms: goals, their status, and the goal tree.

| # | Stage ID | Name | In terms of goals |
|---|---|---|---|
| 1 | `ordinary-world` | Ordinary World | The hero's life before the story's top-level goal exists. Any goals here are small and belong to the old life. |
| 2 | `call-to-adventure` | Call to Adventure | The top-level goal is created, often handed over or forced on the hero by someone else. |
| 3 | `refusal-of-the-call` | Refusal of the Call | The goal exists but is not taken up: it is abandoned at once, or left idle while an older goal is defended. |
| 4 | `meeting-the-mentor` | Meeting the Mentor | A preparation. The hero is equipped, taught, or pushed, and the top-level goal is accepted. |
| 5 | `crossing-the-threshold` | Crossing the Threshold | The hero commits. The goal is now pursued in a world with new rules, and turning back has a cost. |
| 6 | `tests-allies-enemies` | Tests, Allies, Enemies | A run of sequences, each with a smaller goal serving the top-level one. New agents enter with goals of their own, some of them secret. |
| 7 | `approach` | Approach to the Inmost Cave | A second preparation, closer to the centre of the opposition. A goal is often raised here: what was a means becomes an end. |
| 8 | `ordeal` | The Ordeal | The hero's goals collide, or the top-level goal comes closest to being lost. The balance of power is at its worst for the hero. |
| 9 | `reward` | Reward | A goal is won. It is often not the top-level goal, or it is won at a price. |
| 10 | `road-back` | The Road Back | What was won is put at risk. The opposing goal, thought lost, is active again. |
| 11 | `resurrection` | Resurrection | The final contest for the top-level goal, usually demanding that the hero give something up. A raised goal and the original one are settled against each other. |
| 12 | `return-with-the-elixir` | Return with the Elixir | The top-level goal has its final status, and the hero returns changed. Goals left open here are loose ends or deliberate ones. |

## Using it

```
Title: Example
Structure: sequence
Spine: heros-journey

# The Briefing

[[id: q2]]

[[stage: meeting-the-mentor]]

[[goal: stop | id: mission | subject: BOND | object: LARGO]]

[[beat: M hands him the file | ahead: M]]
```
