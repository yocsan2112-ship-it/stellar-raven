# Release review — 2026-09-14

## Verdict

**APPROVED.**

I found no actionable defect in the current release diff.
The prior boundary finding is resolved.
The six audit files are publishable.

Root must run the final baseline gates after this review.
I did not rerun the full build or full test suite.

Fixed point: `da4edefebb5d48929ef587356517f9da090a9a2c`.

## Scope

The review covered these release changes:

- `eval/qa/lint-corpus.mjs`
- `test/qa-corpus-lint.test.mjs`
- `.agents/TODO.md`
- `.agents/rounds/2026-09-14-truth-maintenance.md`
- `research/audits/2026-09-14-audit-independent-review.md`
- `research/audits/2026-09-14-docs-index-recheck.md`
- `research/audits/2026-09-14-drift-review.md`
- `research/audits/2026-09-14-golden-freshness-review.md`
- `research/audits/2026-09-14-improvements-review.md`

I made no source, staging, commit, push, or deployment change.
This report is the only file that I changed.

## Reconciled finding

The earlier review found missed active references at punctuation and Markdown boundaries.
It also found a false warning for a terminal period after `improvements/resolved.json`.

The current matcher recognizes backticks, parentheses, commas, and semicolons.
It does not require whitespace after a comma or semicolon.
It exempts only `improvements/resolved.json` with an optional terminal period.
Other `improvements/` paths still require the symmetric caution.

The current tests add nine boundary cases.
They cover active Markdown references, mixed references, exact receipts, and sentence punctuation.
All 37 focused tests pass.

An independent nine-case probe also passed.
It covered these behaviors:

- An active path in backticks warns.
- An active path in parentheses warns.
- A mixed semicolon string without whitespace warns.
- A mixed comma string without whitespace warns.
- A mixed backtick string warns.
- An exact resolved receipt in backticks does not warn.
- An exact resolved receipt in parentheses does not warn.
- An exact resolved receipt with a terminal period does not warn.
- A resolved receipt followed by an active sentence reference warns.

The earlier Medium finding is closed.

## Protected surfaces

The tracked diff contains only the three named tracked files.
The six named September 14 audit files remain untracked.
The Git index is unchanged.

The protected-surface comparison against `HEAD` returned no diff.
It covered the golden corpus, scoring gates, manifest, super-spec, pins, inventory, and runtime catalog code.

Therefore, this release has no golden, scoring, pin, or exposure change.
The rejected Scout drift candidate remains outside the primary tree.

The new source-metadata follow-up is present in `.agents/TODO.md`.
It names the dead CLI link and the two dated sibling facts.
It requires the `golden-truth` workflow before a later corpus change.

## Report publishability

The six audit files are publishable as dated evidence.
Their conclusions include clear limits and separate source deployment from index ingestion.
They also keep drift rejection separate from the lint release.

Earlier direct scans found no secret in the six files.
Whitespace checks also passed for all six files.

The reports reference temporary evidence under `/tmp` and `/private/tmp`.
The referenced evidence existed during this review.
The drift report states that the operating system can remove it.
The reports preserve the important results needed after removal.

## Independent verification

| Command or check | Result |
|---|---|
| `npx vitest run test/qa-corpus-lint.test.mjs` | PASS: 37 tests in one file |
| Nine-case direct boundary probe | PASS: nine of nine |
| `npm run eval:qa:lint -- --stale` | PASS: 0 errors and 60 warnings |
| `git diff --check` | PASS |
| Protected-surface diff against `HEAD` | PASS: no diff |
| Main Git index check | PASS: no staged diff |

I did not rerun the full build, typecheck, or full test suite.
Root will run those final gates against the current diff.

## Release decision

The release review is complete.
The current patch is ready for the final root validation gates.
