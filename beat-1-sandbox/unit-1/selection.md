# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/31

**Verdict output**

Issue-by-issue grading

Issue #31 — "Add integration tests for the full safety middleware chain"

| Check | Grade | Evidence |
|---|---|---|
| Repo not archived | pass | isArchived: false |
| Maintainer alive | pass | Most recent commit: Andrew Burke, 2026-09-16 |
| Repo in active use | pass | Last push 2026-09-16, 11 days ago |
| Bounded scope | pass | Single file to add (tests/integration/test_safety_middleware.py), covering four well-defined layers — not a tracking issue |
| Not a support question | pass | Concrete enhancement: add integration tests with pass/fail fixtures for each safety layer |
| No active assignee | pass | assignees: [] |
| No open linked PR | pass | Timeline: [] |
| No unanswered active claim | pass | No comments; Path Review house rule applies |
| AI contribution not banned | pass | No policy files; PR template silent on AI |
| Feature request has maintainer buy-in | pass | Carries "enhancement", "safety", "tests", and "tier-2" labels — all maintainer-seeded |
| Good-first-issue label (preferred) | fail | Labels: enhancement, safety, tests, tier-2 — no "good first issue" |
| Maintainer responsiveness sample (preferred) | fail | No Owner/Member/Collaborator replies in sampled issues |
| Reproduction steps present (preferred) | fail | Enhancement, not a bug |

Verdict: ACCEPT (all 10 required checks pass; 0 of 3 preferred)

Ranked read-out: All three candidates (#31, #30, #33) accepted with 0 preferred checks each, ranked by fit profile (Python/backend preference, AI/ML tooling interest, avoid deep frontend). #1 — Issue #31: Python, backend, tier-2 (4–7 hours, lowest effort of the three), and the task directly exercises the AI safety stack (prompt defense → content filter → bias detector → PII scrubber). Testing infrastructure is exactly the kind of AI/ML tooling depth the fit profile is looking for, and the scope is the most self-contained of the three.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/31",
  "checks": [
    {"name": "Repo not archived", "grade": "pass", "evidence": "isArchived: false from GitHub API"},
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Most recent commit by Andrew Burke on 2026-09-16, 11 days ago (within 180 days)"},
    {"name": "Repo in active use", "grade": "pass", "evidence": "Last push 2026-09-16T21:50:20Z, 11 days ago (within 365 days)"},
    {"name": "Bounded scope", "grade": "pass", "evidence": "Single file to add (tests/integration/test_safety_middleware.py) covering four safety layers; not a tracking issue"},
    {"name": "Not a support question", "grade": "pass", "evidence": "Concrete enhancement: add integration tests with pass/fail fixtures for each safety layer"},
    {"name": "No active assignee", "grade": "pass", "evidence": "assignees: []"},
    {"name": "No open linked PR", "grade": "pass", "evidence": "Timeline cross-reference events: []"},
    {"name": "No unanswered active claim", "grade": "pass", "evidence": "No comments in thread; Path Review house rule also applies"},
    {"name": "AI contribution not banned", "grade": "pass", "evidence": "No CONTRIBUTING.md, no AI_POLICY.md; PR template is silent on AI use"},
    {"name": "Feature request has maintainer buy-in", "grade": "pass", "evidence": "Carries maintainer-seeded labels: enhancement, safety, tests, tier-2"},
    {"name": "Good-first-issue label", "grade": "fail", "evidence": "Labels are enhancement, safety, tests, tier-2 — no good-first-issue label"},
    {"name": "Maintainer responsiveness sample", "grade": "fail", "evidence": "All comments in sampled issues #62 and #53 have authorAssociation: NONE; no Owner/Member/Collaborator replies"},
    {"name": "Reproduction steps present", "grade": "fail", "evidence": "Enhancement request — no reproduction steps provided"}
  ],
  "verdict": "accept"
}
```

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Smoke run (`--limit 3`): 3/3 agreement.
2. First full run: 18/20 agreement, category floor met (claimed 4/4, clear-accept 7/8, dead-repo 3/3, policy 1/1, scope 3/4). Disagreements on issue-19 (gold `accept`, my rubric said `reject`) and issue-20 (gold `reject`, my rubric said `accept`).
3. Debug re-run (`--only issue-19,issue-20`, pre-fix): 0/2 agreement, confirming both disagreements from the full run.
4. Debug re-run (`--only issue-19,issue-20`, post-fix): 2/2 agreement, after revising the "Bounded scope" pass condition and adding the "Feature request has maintainer buy-in" check.
5. Final full run (`--save-run eval-run.txt`): **20/20 agreement (bar: 18/20: PASS)**, category floor fully met (claimed 4/4, clear-accept 8/8, dead-repo 3/3, policy 1/1, scope 4/4). This score matches the `agreement` line in the committed `eval-run.txt`.

**Issue analysis**

`issue-19`. Gold label: `accept`. My rubric's result (final version): `accept`.

The first version of my rubric rejected this issue on the "Bounded scope" check, because the issue body is a numbered list: "There are two potential causes which should be fixed: 1. The matchers are slow... 2. UI update is waiting..." followed by "Additional suggestions: 1... 2... 3...". My original pass condition treated any numbered list as evidence of an umbrella/tracking issue and failed it outright.

Rereading the bundle, the two "potential causes" are competing diagnoses of a single bug (a UI freeze), not separate deliverables, and the three "additional suggestions" are explicitly labelled as optional extras, not required sub-tasks. The issue asks for one thing — fix the freeze — with some diagnostic reasoning and optional stretch ideas attached. I revised the "Bounded scope" pass condition to fail only when an issue is explicitly framed as a tracking issue whose listed items are meant to become separate PRs, and to treat a bug report's candidate root causes or labelled-optional suggestions as still bounded. Under the revised condition, "Bounded scope" passes, and since every other required check on this issue also passed, the verdict is `accept`, matching gold.

**Check rationale**

From `rubric.md`:

> Feature request has maintainer buy-in | Issue type (bug vs. feature request), labels, comment thread, and maintainer responsiveness sample | If this is a bug report, pass automatically. If this is a feature/enhancement request, pass only if the thread shows a maintainer comment, or the issue carries a maintainer-applied label beyond default (e.g. "enhancement", "accepted"), showing the maintainers have acknowledged it. Fail if it is a feature request with zero maintainer engagement and no such label — especially when the maintainer responsiveness sample shows the repo typically replies within a few days. | required

I added this check after `issue-20` (gold `reject`) passed every original required check but was still a bad first issue: a feature request opened by a bot account (`cursor[bot]`, `authorAssociation: NONE`), with zero comments and zero labels, in a repo whose maintainer-responsiveness sample showed replies in well under a day. None of my original checks (which covered maintainer life, repo health, scope, and existing claims) could see that gap between "the repo is healthy and responsive" and "nobody has actually looked at this specific request." A fast-responding maintainer ignoring a feature request for days is itself a signal that the request has not been accepted, and a newcomer who builds it risks a PR nobody wants merged.

**Trade-offs**

This check re-ran `issue-20` from a false `accept` to the correct `reject` (confirmed with `--only issue-19,issue-20` after adding it) without changing the verdict on any of the other 19 scored issues, including `issue-19`, which is a bug report and so passes this check automatically regardless of maintainer engagement. The trade-off is that this check will reject a feature request the moment maintainer engagement is genuinely absent, even if the request is well-scoped and would likely be welcomed — it cannot distinguish "not yet reviewed" from "reviewed and ignored." I accept this miss: for a first contribution, waiting for at least one sign of maintainer interest is a safer default than gambling on an unreviewed ask, especially in a high-volume repo where a fast responder's silence is a stronger signal than it would be in a slow-moving one.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. I have professional backend experience (Java-based distributed systems at Amazon) and currently work at a healthcare data company, so I'm comfortable with backend Python and specifically interested in AI safety and data-handling work. Issue #31 is Python, backend, and directly exercises a four-layer safety pipeline (prompt defense, content filter, bias detector, PII scrubber) — close to work I already do. It's tier-2, estimated at 4–7 hours, which fits comfortably in the time I have for this unit.

2. My skill correctly verified the mechanical facts: the repo is active and not archived, the issue is unassigned with no open linked PR or unanswered claim, the maintainer-seeded labels (`enhancement`, `safety`, `tests`, `tier-2`) show the maintainer already wants this built, and nothing in the repo's contribution policy rules out AI-assisted work. What the rubric could not weigh is my own comparative interest across the three accepted candidates: #31, #30, and #33 all passed every required check, so the choice of which one is the *best* fit — not just an acceptable one — came down to my own judgment about workload (tier-2 vs. two tier-3s) and which task teaches me the most about safety-layer testing, which the rubric can rank by fit profile but can't fully substitute for my own read of "what do I actually want to spend my first PR on."

3. I expect claiming this to be low-friction: the issue has no assignee, no linked PR, and no existing claim comments, and the Path Review house rule means even if a classmate has also expressed interest, claiming costs nothing. The main anticipated difficulty is technical rather than social — writing integration fixtures that meaningfully exercise all four safety layers (not just call them) will take some upfront reading of `safety/content_filter.py` and `rag/generator/review_generator.py` to understand how the layers actually chain together before I can write realistic pass/fail cases.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
