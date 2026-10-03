Explains: v1.1.0

Answers for a person asking why a play-style summary came out as it did. The shared method is `docs/_games/approach.md` and `docs/_games/log-contract.md`. This page covers only the choices this skill makes.

## Why there is no single score

This skill keeps the three readings side by side and adds the progression and resource counts from the export. It does not blend those figures into one number, and it does not name a kind of player. A number or a label in the request is not the summary.

## Why a missing reading stops the summary

The summary is the three readings together. If one reading was not supplied, this skill does not build a play style from the other two, and it does not invent the missing reading.

## Why design events are not measured again

Each reading already measured the design events for its construct. This skill takes those scores as given. Measuring the same events again would be a second result, not a summary.

## Why progression and resource are included

Those categories already have a meaning in the export. This skill counts their statuses and flows and places the counts next to the three readings. A note may connect a progression or resource event to a reading only when that reading names the session. Otherwise the counts stay side by side and the note does not invent the link.
