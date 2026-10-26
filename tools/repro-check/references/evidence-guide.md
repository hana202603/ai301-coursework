# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In an eval bundle, the repo-facts block (framework/dependency
versions, pinned commit) and the repro report's own environment section. In
live mode, the issue thread (if a version is named there) and the draft repro
report's environment section.

What good looks like: The report names the actual runtime/dependency versions
used to reproduce. If those versions differ from what the repo-facts block or
the issue text states, the report calls out the mismatch explicitly instead of
staying silent about it.

## Steps

Where it lives: In an eval bundle, the repro report's numbered
reproduction-steps section. In live mode, the draft repro report file.

What good looks like: Every step names a concrete, executable action (an
actual command, an actual input value or file) starting from a stated initial
state and ending at the point where the described behavior appears. No step
requires the reader to guess or infer an unstated command.

## Behavior shown

Where it lives: In an eval bundle, the repro report's output/artifact section,
read against the issue-context section of the bundle. In live mode, the draft
repro report's pasted output, read against the live issue body.

What good looks like: The pasted output (error text, stack trace, log line,
failing test name) carries the same failure signature the issue describes —
same function, same message, same exit condition — not merely a
superficially similar error surfacing from a different code path.

## Honesty

Where it lives: In an eval bundle, the repro report's stated conclusion line,
read against its own artifacts section. In live mode, the draft repro report's
conclusion sentence, read against what it actually pasted as evidence.

What good looks like: The conclusion claims no more than the artifacts
support. An honest "could not reproduce" that lists what was tried and what
happened instead is just as valid a pass as a "reproduced" claim backed by
matching output.

## Comms

Where it lives: In an eval bundle, the repo-facts block's policy fields
(contribution policy, AI-disclosure requirement), read against both the claim
comment and repro report text. In live mode, the repo's CONTRIBUTING.md, PR
template, or AI-use policy file, read against the draft claim and repro
comments.

What good looks like: The comment states its intent or results in the repo's
own terms, not boilerplate lifted from elsewhere. If the repo requires
disclosing AI assistance, the comment discloses it plainly rather than
omitting or burying it.