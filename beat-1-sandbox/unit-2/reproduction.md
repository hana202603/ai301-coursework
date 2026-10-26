# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

hana202603

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/31#issuecomment-5864773085

Hi, I'd like to pick this up as a first contribution. The issue asks for
integration tests covering the full safety middleware chain (prompt
defense -> content filter -> bias detector -> PII scrubber), with
pass/fail fixtures for each layer.

Before writing the test file, my plan is to read through
`safety/content_filter.py` and `rag/generator/review_generator.py` to
understand how the four layers actually chain together, so the
fixtures exercise the real pipeline rather than just calling each
layer in isolation. I'll follow up once I have a first draft of the
test structure.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/31#issuecomment-6410053596

Environment: Python 3.14.3, macOS 15 (Darwin 25.3.0, arm64, Apple Silicon),
repository at hana202603/pathreview-ai301-fa26-s3 (fork of
codepath/pathreview-ai301-fa26-s3), installed via make setup into a
local .venv. Docker services: postgres:16-alpine, redis:7-alpine,
and chromadb/chroma:0.4.22 (the latter needed a command override in
docker-compose.yml to skip its entrypoint's forced chroma-hnswlib
reinstall, which otherwise pulls a NumPy 2.x build incompatible with
this chromadb version's np.float_ usage - an environment-specific
issue unrelated to the safety middleware itself).

Steps:

1. Confirmed, by searching the codebase, that none of the four safety
   modules (safety/prompt_defense.py, safety/content_filter.py,
   safety/bias_detector.py, safety/pii_scrubber.py) are imported or
   called anywhere outside their own unit tests. Equivalent greps for
   PromptDefense, ContentFilter, BiasDetector, and PIIScrubber returned
   matches only inside their own unit test files and their own
   definitions - never from rag/generator/review_generator.py, agent/,
   or api/.

2. Wrote tests/integration/test_safety_middleware.py, adding a
   run_safety_pipeline() helper that chains the four layers in the
   order the issue names (prompt defense -> content filter -> bias
   detector -> PII scrubber), since no such chain exists in the
   application code to import.

3. Added 12 tests under @pytest.mark.integration, covering: a clean
   pass-through case, a pass/fail pair for each of the four layers, a
   combined case triggering all four layers together, and an empty-
   string edge case. One test
   (test_ignore_instruction_requires_leading_newline) demonstrates a
   real gap directly: PromptDefense.is_injection_attempt()'s
   "Ignore/Forget/Disregard/Override" pattern only matches when the
   instruction follows a leading newline character, so the identical
   sentence is caught or missed purely based on that leading newline.

4. Ran: make test-integration

Expected: a test run exercising all four layers together, each with at
least one passing and one failing (correctly-detected) fixture.

Actual: 12 passed in 0.16s. All four layers behaved individually as
their own unit tests describe once invoked with inputs that match their
specific regex patterns exactly (several patterns are narrow - e.g.
ContentFilter's harmful-language patterns require exact adjacency
like "worthless person", not "worthless ... as a person"; BiasDetector
requires the literal word "old", not "older"). No code change was made
to the safety modules themselves; this submission only adds the missing
integration test file, per the issue's request.

The issue's premise is confirmed as stated: unit tests existed for each
component in isolation, but no test (and no application code path)
exercised the full chain together. This submission fills exactly that
gap, with pass/fail fixtures for all four layers as the issue requested.

Test file (committed to this fork): https://github.com/hana202603/pathreview-ai301-fa26-s3/blob/42fa9dda31451b7c730384fefbbd1dbcbd018072/tests/integration/test_safety_middleware.py
Commit tested: 42fa9dda31451b7c730384fefbbd1dbcbd018072

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (--limit 3): 3/3 agreement.
2. First full run: 16/20 agreement, below the 18/20 bar (categories: clear-accept 4/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). Disagreements on pkg-05, pkg-07, pkg-11, pkg-12 - all gold accept, my rubric said reject, failing on steps-rerunnable and/or claim-promises-not-asserts.
3. Debug re-run (--only pkg-05,pkg-07,pkg-11,pkg-12, pre-fix): confirmed the disagreements (2/4 agreement on a repeat pass, with some run-to-run model variance on pkg-07/pkg-11, but pkg-05 and pkg-12 failing consistently).
4. Revised steps-rerunnable to accept precisely-described (not necessarily verbatim) inputs and steps that reference detail already shown in the issue thread, and revised claim-promises-not-asserts to allow a factual, evidence-backed "I reproduced this" statement rather than treating any statement of reproduction as overclaiming.
5. Debug re-run (--only pkg-05,pkg-07,pkg-11,pkg-12, post-fix): 4/4 agreement.
6. Canary re-run (--only pkg-06,pkg-13,pkg-19, checking unfollowable-comms and no-evidence for regressions): 2/3 agreement. pkg-19 flipped from a correct reject to an incorrect accept - the loosened claim-promises-not-asserts let through a boilerplate claim promising "I will fix it within 2 days guaranteed."
7. Revised claim-promises-not-asserts again to explicitly fail a promised delivery timeline or guaranteed outcome, without touching the fix from step 4.
8. Re-run of all seven affected packages (--only pkg-05,pkg-06,pkg-07,pkg-11,pkg-12,pkg-13,pkg-19): 7/7 agreement - the four original disagreements fixed, the three canaries held.
9. Final full run (--save-run eval-run.txt): 19/20 agreement (bar: 18/20: PASS), categories: clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 3/4. Remaining disagreement: pkg-16 (gold reject, my rubric accept). This score matches the agreement line in the committed eval-run.txt.

**Package analysis**

pkg-16. Gold label: reject (category: wrong-target). My rubric's result: accept.

The issue states plainly that the reporter "confirmed the bug on the latest version and on the main branch" (pandas v3.0.5, Python 3.14.6). The candidate repro report instead ran on pandas 1.5.3 and Python 3.10.12 - several major releases behind - and never acknowledges that gap. It states, without qualification: "The crash the issue describes is confirmed: index creation with a tuple name succeeds and rename_axis with the same tuple fails at runtime."

My rubric let this through for two reasons. First, environment-recorded's pass condition only asks whether the environment is stated with enough specificity for a stranger to recreate it - it says nothing about whether that environment matches what the issue's own report confirms as the target. The candidate report states its version precisely (pandas 1.5.3, Python 3.10.12, Ubuntu 22.04), so it satisfies the check literally, even though the version itself is the problem. Second, behavior-matches-issue compares the shown failure signature (a ValueError at rename_axis) against the issue's described symptom (a runtime failure at rename_axis) and finds them superficially the same - but the check never cross-references the environment against the issue's "confirmed on latest and main" note, so it cannot see that an old-version ValueError might come from an entirely different code path than the one the maintainer's own comment points to (Index.set_names, on the current codebase).

**Check rationale**

From rubric.md:

environment-recorded | The repro report's environment/setup section, checked against the repo-facts block's version info | Pass: the report states concrete environment details (OS/runtime version, dependency versions, any required config or flags) precise enough for a stranger to recreate the same setup. Fail: vague statements like "set up the project locally" with no specifics, or no environment mentioned at all. | required

I wrote this check to catch the failure mode the lecture's proof families named directly: a report with no environment record at all, like the vague "set up the project" placeholder. It deliberately does not require the report's environment to match any particular target version - only that whatever environment was used is stated precisely enough to be recreated. That looser bar is what let pkg-05, pkg-07, pkg-11, and pkg-12 pass cleanly (their environments were concrete but not identical to the issue's own version), and it is also exactly why pkg-16 slipped through: its environment statement is just as concrete as those, but it happens to be the wrong environment for the bug being investigated.

**Trade-offs**

This check's current wording gives up the ability to catch a silent version deviation - a report that states its environment honestly and precisely, but never checks that environment against what the issue itself confirms as the reproducing target. pkg-16 is exactly this case: nothing about the check's stated pass condition is violated, yet the version gap is the entire reason gold rejects it.

I accept this miss for now rather than tightening the check, because the obvious fix - requiring the stated environment to match or be no older than the issue's confirmed target - would risk a new false rejection on the "honest cannot-reproduce" packages the rubric already handles well (pkg-09, pkg-10), where running on a different environment on purpose, and naming the difference, is precisely what makes those reports good. A version-matching rule would need to distinguish "different environment, acknowledged and reasoned about" from "different environment, asserted as if it were the target one," and my current check has no such distinction. Tightening it without that nuance would trade a wrong-target miss for a new set of false rejects on legitimate control-run reproductions.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
