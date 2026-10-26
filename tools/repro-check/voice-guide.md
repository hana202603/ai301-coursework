# Voice guide: how I talk upstream

## Who I am in threads

I'm a backend engineer with professional distributed-systems experience,
making my first open-source contribution in this repo. I'm being careful and
precise rather than fast, and I say plainly when something is a verified fact
versus a guess I haven't confirmed yet.

## Rules I write by

### Rule: Promise investigation, not a fix

A claim comment says what I'm going to look into, never that I've already
fixed or fully diagnosed anything.

- Wrong: "I'll have this fixed by tomorrow."
- Right: "I'm going to investigate this and report back what I find."

### Rule: State uncertainty as uncertainty

If I haven't confirmed something, I say so instead of writing it as settled
fact.

- Wrong: "This is definitely caused by the PII scrubber skipping nested
  fields."
- Right: "My working guess is the PII scrubber skipping nested fields, but I
  haven't confirmed that yet."

### Rule: No timelines I can't guarantee

I don't promise dates. I promise the next update.

- Wrong: "I'll have a PR up by Friday."
- Right: "I'll post an update once I've finished reproducing this."

### Rule: Say exactly what I ran

Vague setup language is not a substitute for the actual command and the
actual commit.

- Wrong: "I set up the project and tested it."
- Right: "I ran `pytest tests/integration/test_safety_middleware.py` against
  commit abc123."

### Rule: Disclose AI assistance plainly, once

If I used AI assistance and the repo's policy requires disclosure, I say so
directly in the comment, not as a buried footnote.

- Wrong: (leaving it out, or mentioning it only if asked)
- Right: "I used Claude Code to help draft this report; the repro steps and
  conclusions were run and verified by me."

## Things I never post

- Never "same as above, can confirm" on a shared issue — I write my own
  reproduction, from my own environment, in my own words, every time.
- Never claim something is fixed when all I've done is reproduce it.
- Never post a claim or repro comment I haven't run through repro-check
  first.