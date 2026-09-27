# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repo not archived | Repo-facts "archived:" line (eval) / archived banner on repo front page (live) | Repo is not marked archived | required |
| Maintainer alive | Repo-facts "last 5 default-branch commits" (eval) / commit list on repo front page (live) | At least one of the last 5 default-branch commits was authored or merged (a bot merging a human PR counts) within the last 180 days | required |
| Repo in active use | Repo-facts "latest release" and "last push to any branch" (eval) / Releases box + front-page commit date (live) | Latest release date OR last push to any branch is within the last 365 days | required |
| Bounded scope | Issue body and comment thread | Fail only if the issue is explicitly framed as a tracking/checklist issue whose listed items are meant to become separate, independent PRs (e.g. links out to sub-issues, or states "tracking issue"). A bug report that lists multiple candidate root causes for one underlying problem, or appends optional "additional suggestions" beyond the core fix, is still bounded: judge scope by the core ask, not by suggestions explicitly marked optional. | required |
| Not a support question | Issue body | Issue describes a concrete bug or feature/change, not a general "how do I use this" question | required |
| No active assignee | Repo-facts "this issue: assignees:" (eval) / Assignees box (live) | Assignees list is empty | required |
| No open linked PR | Repo-facts "linked PRs:" with state (eval) / Development box + thread mentions (live) | No linked or thread-mentioned PR is currently open | required |
| No unanswered active claim | Comments section (eval) / issue thread (live) | No claim comment ("I'll take this" / "working on this") within the last 30 days that a maintainer has not refuted or reassigned. (Path Review house rule in scope.md overrides this check in live mode on the course's Path Review repo: other students' claims never fail this check there.) | required |
| AI contribution not banned | Repo-facts "contribution policy" line (eval) / CONTRIBUTING.md, AI_POLICY.md, PR templates (live) | Policy does not state an outright ban on AI-generated or AI-assisted contributions. Conditions (disclosure, human review, testing) pass; silence passes. | required |
| Feature request has maintainer buy-in | Issue type (bug vs. feature request), labels, comment thread, and maintainer responsiveness sample | If this is a bug report, pass automatically. If this is a feature/enhancement request, pass only if the thread shows a maintainer comment, or the issue carries a maintainer-applied label beyond default (e.g. "enhancement", "accepted"), showing the maintainers have acknowledged it. Fail if it is a feature request with zero maintainer engagement and no such label — especially when the maintainer responsiveness sample shows the repo typically replies within a few days. | required |
| Good-first-issue label | Issue labels | Issue carries a "good first issue" or equivalent label | preferred |
| Maintainer responsiveness sample | Repo-facts "maintainer first-response sample" (eval) / recent issues sorted by update (live) | At least one Owner/Member/Collaborator reply appears within 30 days in the sample | preferred |
| Reproduction steps present | Issue body | Bug report includes concrete steps to reproduce | preferred |

## Verdict rule

Accept if and only if every required check passes. A grade of `unclear`
on a required check counts as `fail` for that check. Preferred checks
never change the verdict; they only rank issues that are already
accepted, ordered by number of preferred checks passed (ties broken by
the fit profile in scope.md). Reject otherwise.
