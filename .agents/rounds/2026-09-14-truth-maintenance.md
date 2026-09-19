# Truth maintenance 2026-09-14

## Scope

Review live drift, all active improvements, related issues and PRs, and required tests and evaluations.
The user requested an audit. Changes are limited to audit evidence and this ledger.
No deployment, upstream messages, finding retirement, or paid evaluation is part of this review.
The initial working tree was clean.

## Lane plan

| Lane | Agent | Scope | Artifact |
|---|---|---|---|
| Coordinator | Current agent, `w3G:p2` | Baseline tests, free evaluations, lint, probes, freshness, synthesis | This ledger |
| Drift | Sol high, `raven-drift-0914`, `w3G:pP` | Isolated regeneration, issue #141, full surface classification, candidate checks | `research/audits/2026-09-14-drift-review.md` |
| Improvements | Terra high, `raven-findings-0914`, `w3G:pQ` | Every active record, current upstream state, original-trigger checks for fix candidates | `research/audits/2026-09-14-improvements-review.md` |
| Golden freshness | Grok 4.6 high, `raven-golden-0914`, `w3G:pR` | Six near-due cases and due consistency triggers | `research/audits/2026-09-14-golden-freshness-review.md` |

The coordinator owns all three spawned panes. Workers cannot spawn children.
Sol handles dense drift analysis. Terra handles the bounded issue and finding census.
Both model identifiers and high effort were confirmed in the local model catalog.
Both agents started successfully through Herdr.

Planned checks: `npm run typecheck`, `npm test`, `npm run build`, `npm run eval:selftest`,
`npm run eval:compile`, `npm run eval:routing -- --gate`, `npm run eval:qa:lint -- --stale`,
`npm run improvements:lint -- --live`, and `npm run improvements:probes -- --include-declined`.
Review the next 28 days of golden due dates. Inspect stored evaluation evidence when relevant.

## Drift verdict

Reject the combined candidate. Issue #141 remains open as of 2026-09-14.
The isolated candidate updates Scout from `1.9.1` to `1.9.51`, adds RWA, and changes the skill pin.
Docs titles increase from 650 to 651. Lumenloop and Docs settings remain unchanged.
The candidate loses strict routing grades and fails 13 of 2,059 unit tests.
All 94 candidate smoke tests pass. The candidate build passes; candidate typecheck did not run.
The routing gate rejects the changed fingerprint; the separate numerical comparison establishes the regressions.
RWA still captures unrelated WASM, RPC, Friendbot, simulation, and balance questions.
The new operation needs an explicit exposure decision. The skill pin still needs its review attestation.
See `research/audits/2026-09-14-drift-review.md` for every changed operation, failed fixture, and candidate hash.
The root independently read Scout OpenAPI `1.9.51` at approximately `2026-09-14T21:13:00Z`.
The RWA state parameter includes `issued-single-holder`.
`GET /api/rwa?state=issued-single-holder&limit=1` returned 200, one row, and 34 matches.
`GET /api/rwa?state=invalid-raven-audit&limit=1` returned 400.
These checks confirm the old state-schema defect is fixed; they do not accept the candidate catalog.

## Eval verdict

Baseline revision: `da4edefebb5d48929ef587356517f9da090a9a2c`.

| Check | Result | Evidence |
|---|---|---|
| `npm run typecheck` | PASS | `/tmp/raven-0914-typecheck.log` |
| `npm test` | PASS: 2,059 tests, 114 files | `/tmp/raven-0914-tests.log` |
| `npm run test:smoke` | PASS: 94 tests, five files | `/tmp/raven-0914-smoke.log` |
| `npm run build` | PASS, dry run only | `/tmp/raven-0914-build.log` |
| `npm run eval:selftest` | PASS | All grader and contract checks passed |
| `npm run eval:compile` | PASS | 338 legacy and 122 extended cases |
| `npm run eval:routing -- --gate` | PASS | `eval/results/routing-2026-09-14T21-07-05-843Z.json` |
| `npm run eval:qa:lint -- --stale` | PASS: 0 errors, 64 warnings | No corpus edits; diff-based gospel check skipped |
| `npm run improvements:lint -- --live` | PASS: 61 findings | `/tmp/raven-0914-improvements-lint.log` |
| `npm run improvements:probes -- --include-declined` | 7 recurring; no errors or fixed candidates | `/tmp/raven-0914-probes.log` |
| `npm run algolia:rule-canary -- --env-file .env --require-env` | PASS: 4 assertions | Rules-on rank 1 for both queries; controls miss and rank 5 |
| `npm run eval:protocol-history` | `source-expired`, exit 1 | `eval/results/protocol-history-2026-09-14T21-07-51-399Z.json` |
| `npm run eval:plan -- eval/qa/results/2026-08-30T03-43-11-variantA.json` | Completed historical diagnostic | 93/100 required coverage; mean on-plan ratio 0.95 |
| `npm audit --json` | 8 affected dependencies: 7 high, 1 moderate | `/tmp/raven-0914-npm-audit.json` |
| `npm audit --omit=dev --json` | 1 moderate affected dependency: `hono` | `/tmp/raven-0914-npm-audit-production.json` |

The baseline routing totals match the committed acceptance totals.
Legacy top-1/3/5: 213/279/312 of 338. Skills: 16/23/23 of 23.
Holdout top-1/3/5: 10/22/26 of 49. Forbidden captures: 11. Holdout passes: 21.
Extended top-1/3/5: 90/110/116 of 122.
These results show baseline stability, not complete retrieval quality.

The historical v1 protocol diagnostic finds 4/8 positives and captures 2/4 controls.
The current v2 contracts refuse scoring because the manifest hash differs from their source epoch.
Do not refresh that hash solely to obtain scores. The existing protocol-history queue controls re-authoring.

The plan regrade used 100 stored August 30 rows, with Sonnet 5 answering and judging.
Its original artifact reports comparability for that historical run only.
It does not measure September 14 answer quality. No new answering or judging calls ran.

The dependency audit reproduces the existing dependency queue item.
Its development-only high findings do not establish production exploitability.
The production graph includes `hono` advisories below version `4.13.5`.
Audit repair suggestions include a major test-tool downgrade and unavailable fixes; do not apply them blindly.
The installed `node_modules/node_modules` is a self-referencing symlink dated September 9.
`npm ls hono --all` returned an empty tree, while `npm explain hono` followed that cycle.
The lockfile and installed `node_modules/hono/package.json` both report `4.13.1`.
Treat dependency-tree output cautiously until a clean dependency installation removes this local anomaly.
This audit preserved the existing installation.

CI at the baseline revision passed on September 11:
https://github.com/stellar-experimental/stellar-raven/actions/runs/34645719853.
The latest daily refresh failed at its deliberate drift gate:
https://github.com/stellar-experimental/stellar-raven/actions/runs/34815420034.
Its September 14 comment reports 18 Scout routing-text changes and 12 schema-only changes.
The old issue body reports an older source snapshot; use the latest comment and fresh regeneration.
The root read back the bot-authored comment:
https://github.com/stellar-experimental/stellar-raven/issues/141#issuecomment-5660180618.

## Golden verdict

All 500 battery cases passed the stale check. Of these, 150 have scheduled due dates.
No scheduled case is overdue on September 14.
The reviewer checked six cases within the next 28 days and recommended no factual edits:

| Case | Due |
|---|---|
| `q-ti-stellar-lab-usage-and-new-ui` | 2026-10-01 |
| `q-builder-content-by-person` | 2026-10-07 |
| `q-comp-yieldblox-oracle-incident` | 2026-10-08 |
| `q-hist-meridian-2026-corrected-venue` | 2026-10-08 |
| `q-hist-x402-stellar-announcement` | 2026-10-08 |
| `q-edge-closed-world-builder-directory-miss` | 2026-10-09 |

The 64 warnings include sourcing guards, missing negative-claim corroboration, and four symmetric-caution warnings.
Warnings need semantic review; their presence alone does not justify changing a golden.

The root inspected all four symmetric-caution warnings.
Their `truth.verified.rootCause` values refer to terminal `improvements/resolved.json` receipts:
`sd-021`, `sd-036`, `sd-039`, `sd-042`, and `sd-047`.
The case notes or verification evidence explicitly retire the former source conflicts.
The lint at `eval/qa/lint-corpus.mjs:534` matches `improvements/` without distinguishing terminal receipts.
These four warnings do not establish missing current cautions.
A future lint repair should distinguish active source conflicts from resolved provenance.
Do not restore expired golden cautions merely to suppress these warnings.
The independent reviewer confirmed all four false positives against the resolved receipts.
The review found one dead Stellar Lab source link and two sibling freshness checks.
The sibling checks concern current x402 board membership and the dated builder population count.
See `research/audits/2026-09-14-golden-freshness-review.md` for exact cases and replacement source.

## Improvements/issues/PR verdict

The active tree contains 61 findings: 58 reported upstream and three declined upstream.
Collections: 29 Lumenloop, seven skills, 20 Docs, four Scout, and one workers-ai-provider.
There are no unfiled verified findings or fixed-upstream deletion candidates.
All seven registered probes still reproduce: `ll-003`, `ll-007`, `sk-005`, `sk-007`, `sk-014`, `sk-015`, `sk-022`.
Probe coverage is 7/61. A green probe command does not verify the other 54 records.
Raven has no open PRs at the initial check. Its open issues are #141 and #40.

Production `GET https://raven.stellar.org/health/skills` returned `ok:true` with 42 checked files.
The stored check ran at `2026-09-14T21:07:17.012Z`.
This proves the reported canary run, not all serving locations.

The `sls-080` monitor passed through the documented direct Scout endpoint.
No local development server was available; this check does not prove the Raven adapter path.
Request: `GET /api/repos/explain`, repository `stellar/stellar-horizon`, question:
`Which Horizon ingestion constant pins the highest supported protocol version, and what is its value?`
The API returned 200 and `MaxSupportedProtocolVersion = 28`.
`generatedAt`: `2026-09-14T21:08:48.422Z`; `answerSource`: `knowledge-note`;
`answerAsOf`: `2026-09-01T00:00:00Z`; `scannedRef`: `82660510ecda7fd365a14d08badb9d85fa22bc32`.
The source at that exact commit returned 200 and defines `MaxSupportedProtocolVersion uint32 = 28` at line 38.
Source: https://github.com/stellar/stellar-horizon/blob/82660510ecda7fd365a14d08badb9d85fa22bc32/internal/ingest/main.go#L38.

### Source versus index reconciliation

The findings reviewer found deployed source corrections for `sd-040`, `sd-041`, and `sd-045`.
The root independently repeated their production page-section queries and found all three old defects still indexed.
The root also fetched the rendered pages and confirmed their corrections.
Decision: source fixed, index stale. None is ready for full resolution.
Grok independently repeated all three production index queries at `2026-09-14T21:20:42.725Z` and confirmed the stale text.
Its earlier web page-search results conflicted with direct HTML reads.
The root repeated direct HTML reads at `21:26:39Z`; Grok repeated them at `21:27:10Z`.
Both direct reads confirmed the corrections. The reviewer withdrew the stale-search refutation.
The independent report preserves both observations and their retrieval limits.
Exact commands, paths, sections, and observations are in
`research/audits/2026-09-14-docs-index-recheck.md`.

### Scout lifecycle reconciliation

The first findings review treated null `products` and `deployments` as defects.
The root rejected that inference because the current response separately encodes explicit unknown deployment.
The root queried the five exact September 8 `sls-024` source-provenance fixtures through production Raven.
Checks ran at `2026-09-14T21:19:17Z` through `21:19:22Z`.
All five now carry `statusSourceUrl`:

| Exact project | Current basis | Source URL |
|---|---|---|
| Scam Flagging System | `human-verified` | `https://docs.google.com/spreadsheets/d/1JCkWZ3X1h6kJKM6ZCZThDshK_whhNiTyGTV8R24Anho/edit` |
| Stellar Pulse | `unverified` | `https://web.archive.org/web/20251013160228/https://stellarpulse.app/` |
| Pactta | `human-verified` | `https://rdap.verisign.com/com/v1/domain/pactta.com` |
| The Blue Marble | `human-verified` | `https://rdap.identitydigital.services/rdap/domain/thebluemarble.io` |
| ChainCred | `human-verified` | `https://github.com/Prince29chouhan/ChainCred` |

Each exact row reports `deployment.network: unknown` and null deployment evidence.
Those fields state unknown deployment; they do not assert a known deployment without evidence.
The requests used `scout.searchProjects({q: <exact project name>, limit:5})`.
Search also returned adjacent rows; only exact-name rows support this table.
These five fixes do not establish population-wide resolution or resolve every canonical product-link residual.
The final review keeps this conclusion scope-limited.
It recommends no successor based only on null fields for `sls-029` or `sls-033`.

## Own-repo todos

All 61 active records and their recorded issue and PR references received review.
Authenticated GitHub reads covered all 27 distinct private Lumenloop backend issues; all remain open.
The seven registered probes and seven targeted candidate checks do not cover every original trigger.

The existing `sd-037` follow-up date has passed.
The root read issue `stellar/stellar-protocol#1981`: CLOSED, NOT_PLANNED, updated `2026-09-14T18:14:06Z`.
Its latest comment was the August 14 stale-bot warning. Closure is not evidence of a fix.
The reviewer checked the original source trigger. The missing protocol proposal index still reproduces.

The existing `sd-027` / `sd-034` follow-up points to closed Docs PR #2367.
ElliotFriend closed it on September 9 with `superseded by #2837`; `mergedAt` is null.
Successor https://github.com/stellar/stellar-docs/pull/2837 remains OPEN with `REVIEW_REQUIRED`.
Update the next-check target to #2837 when maintaining the queue.

Docs PR https://github.com/stellar/stellar-docs/pull/2850 is OPEN with `REVIEW_REQUIRED`.
It documents `--enable-core-manual-close` for `sd-044`. Two factual review comments still need author action.

Raven issue #40 still needs the existing authenticated production copy acceptance check.
The owner's September 9 comment retains the 8,000-character limit and rejects persistent demonstration chat history.
The root read this comment directly. This audit did not create a paid playground response.

## Decisions

GitHub closure does not prove a live fix. Original-trigger evidence controls each conclusion.
Candidate artifacts stay outside the primary working tree.

## Next work, in order

1. Evaluate Scout changes separately from the Docs title and skill pin changes.
   Start with a temporary, RWA-excluded ablation to isolate the remaining Scout changes.
   Keep labels, scoring, and accepted gate values unchanged. This experiment does not authorize source adoption.
2. Resolve the explicit RWA exposure decision and general routing failures before updating frozen counts or examples.
   Require the existing 11 scoring checks, exact case comparisons, and independent acceptance review.
3. Repeat the three original Docs index queries after ingestion. Keep the findings unresolved until the index converges.
4. Update the stale `sd-027` / `sd-034` tracker reference to PR #2837 during authorized queue maintenance.
   Seek an owner decision for the stale-bot-closed, still-reproducing `sd-037` finding.
5. Complete the remaining Scout provenance and canonical-link checks before any lifecycle change.
6. Repair the four lint false positives and the dead Lab source link in scoped follow-up changes.
   Review the two dated sibling facts. Do not restore expired cautions or change historical answers to current facts.
7. Repair dependencies through a clean installation and reviewed upgrades. Test each upgrade against the baseline.
8. Re-author source-expired protocol-history contracts only through their existing queue and acceptance rules.
   Run focused QA only after source selection and a separate paid-run contract receive approval.

Broad paid QA is not the next useful test. Free candidate checks already show concrete acceptance failures.
The historical plan regrade cannot replace a current QA run after source acceptance.
The Docs title inventory remains below the 1,000-record ceiling; monitor growth before that limit.

## Final checklist

- All three lane reports completed. The root reconciled source/index and Scout unknown-state conclusions.
- Baseline tests, free evaluations, and bounded live probes completed with the limits above.
- Independent rendered-page reconciliation completed. Every independent finding has a recorded disposition.
- The root verified the candidate manifest and test-result hashes and confirmed 2,046 passing and 13 failing candidate tests.
- Whitespace and secret checks passed for all six new audit files through a temporary Git index.
- The main Git index remains unchanged. Only the six audit Markdown files are untracked.
- All three agents completed. The coordinator closed only owned panes `w3G:pP`, `w3G:pQ`, and `w3G:pR`.
- The isolated candidate remains available at the path recorded in the drift report. No evidence directory was deleted.
- No source change, finding-state change, commit, deployment, upstream write, or new paid QA run occurred.

## Authorized release follow-up

The user then requested a commit, push, deployment, and obvious useful follow-up work.
This authorization supersedes the audit-only boundary for this follow-up, not the historical observations above.

The release fixes the lint exemption for exact `improvements/resolved.json` references.
Active references still require a caution, including a reference mixed with a resolved receipt in the same string.
Fifteen regression cases cover the distinction and Markdown or punctuation boundaries.
No golden, scoring rule, source pin, or exposed operation changes.
The work queue now targets Docs PR #2837 and records the still-reproducing, stale-bot-closed `sd-037` decision.

The first validation passed 2,065 unit tests, including 28 corpus-lint tests. Typecheck and build passed.
The reviewer found missed active references inside Markdown or adjacent punctuation.
The root corrected the parser and added nine boundary cases, including sentence punctuation.
The corpus lint passes with zero errors and 60 warnings, down from 64.
The four removed warnings correspond to the independently verified resolved receipts.
The remaining source-link, source-acceptance, dependency, and lifecycle work retains its separate acceptance requirements.

Independent release reviewer: Sol high, `raven-release-review`, owned pane `w3G:pS`.
This lane reviews the implementation and audit publication before the commit.
The release preserves Scout `1.9.1` and the current skill pin. It does not accept the rejected drift candidate.

The reviewer approved the final parser after independent boundary probes and all 37 focused tests passed.
Final root validation against that parser passed: typecheck, 2,074 unit tests, build, and corpus lint.
The corpus lint reports zero errors and 60 warnings. No golden changes occurred.
The release routing gate and evaluation self-tests passed. All 94 smoke tests also passed.
Review evidence: `research/audits/2026-09-14-release-review.md`.
The coordinator closed the owned review pane after completion.
