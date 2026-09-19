# Improvements review — 2026-09-14

## Result

The active queue has 61 records: 58 `reported-upstream` and three
`declined-upstream` records. There are no `proposed`, `verified`, or
`fixed-upstream` active records. There are no unfiled verified records.

The coordinator ran `npm run improvements:lint -- --live`. It passed all 61
records. The coordinator also ran the registered probes. All seven probes
recurred: `ll-003`, `ll-007`, `sk-005`, `sk-007`, `sk-014`, `sk-015`, and
`sk-022`. A recurrence is evidence of an unresolved trigger. It is not a
status change by itself.

I read all 61 recorded issue references and all six recorded pull request
references. I used authenticated, read-only `gh api` for all 27 distinct
`lumenloop/lumenloop-backend` issues. All 27 are open. Their latest comments
are Raven-authored, or the issue has no comment.

GitHub closure and merge state did not determine any finding status. I ran
the source and original-index checks required by the three Docs findings. Their
source pages are fixed, but their production Docs index still serves the old
text. I also rechecked the closed protocol and Scout candidates with their
current field semantics.

## Priority definitions

| Priority | Meaning |
|---|---|
| P1 | A source/index split, closed-unfixed record, or active upstream change needs a direct check. |
| P2 | The record has a verified recurrence, scope-limited improvement, or concrete watch item. |
| P3 | The tracker is open and quiet. |

## Direct rechecks

| Finding | GitHub signal | Direct recheck | Result | Required next action |
|---|---|---|---|---|
| `sd-040` | `stellar/stellar-docs#2768` and PR `#2849` closed completed | The source page now returns `Result<Address, ConversionError>`. Production Raven still returns `Address::from_xdr(&env, &bytes).unwrap()` in one affected section of seven complete sections. | The original index trigger still reproduces. | Keep reported status. Verify a fresh index after crawl or reindex. |
| `sd-041` | `stellar/stellar-docs#2769` and PR `#2853` closed completed | The source page has current memo wording. Production Raven still returns `We used memos in the past` in one affected section of 15 complete sections. | The original index trigger still reproduces. | Keep reported status. Verify a fresh index after crawl or reindex. |
| `sd-045` | `stellar/stellar-docs#2773` and PR `#2851` closed completed | The source page qualifies loopback HTTP. Production Raven still returns the unqualified HTTPS statement in one affected section of 35 complete sections. | The original index trigger still reproduces. | Keep reported status. Verify a fresh index after crawl or reindex. |
| `sd-037` | `stellar/stellar-protocol#1981` closed `NOT_PLANNED` by a stale bot | The current root README names CAPs and SEPs only. The limits README names SLPs but has no proposal index. | The source trigger still reproduces. | Create a successor or reopen path only after owner review. Do not mark fixed. |
| `sls-024` | Both `stellar-scout#9` and `stellarlight#494` are closed | All five September 8 fixtures now have `statusSourceUrl`. Each has `deployment.network: "unknown"` with null evidence fields. The OpenAPI defines this as correct unknown semantics. | The exact source-provenance trigger no longer reproduces. | Record a scope-limited improvement. Check QCAD and GLOUSD links, plus population coverage, before any broader conclusion. |
| `sls-029` | `stellarlight#514` and consolidated `#742` are closed | `products: null` means no modelled product record and is explicitly unknown. `deployment.network: "unknown"` means no evidence either way. Lightecho's record states its missing contract ID. | Null fields alone do not reproduce an unsafe positive claim. | Do not recommend a successor from null fields. Recheck only an unsafe product or network claim. |
| `sls-033` | `stellarlight#519` and consolidated `#742` are closed | Exact `type=Wallet` returns 71 rows. The schema defines null `productKind` as not yet classified and null `availability` as not curated. | Null fields alone do not reproduce a false availability or taxonomy claim. | Do not recommend a successor from null fields. Recheck an unsafe classification or duplicate claim. |

The Docs index reads ran through production Raven at `2026-09-14T21:16:57Z`.
The five Scout fixture reads ran from `2026-09-14T21:17:59Z` through
`2026-09-14T21:18:03Z`. Root repeated those five reads through Raven from
`21:19:17Z` through `21:19:22Z` with the same result.

## Reproducible live checks

These are the exact source and index obligations. A source-page result alone
does not resolve a finding whose original trigger is an indexed Docs read.

| Finding | Source URL and command | Original index or API command |
|---|---|---|
| `sd-040` | `curl -LsS https://developers.stellar.org/docs/build/guides/conversions/address-conversions` | `await stellarDocs.get_doc_page_sections({ path: "/docs/build/guides/conversions/address-conversions", includeContent: true })`; inspect `#xdr-conversions-in-smart-contracts`. |
| `sd-041` | `curl -LsS https://developers.stellar.org/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos` | `await stellarDocs.get_doc_page_sections({ path: "/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos", includeContent: true })`; inspect the page-root lead. |
| `sd-045` | `curl -LsS https://developers.stellar.org/docs/build/guides/dapps/frontend-guide` | `await stellarDocs.get_doc_page_sections({ path: "/docs/build/guides/dapps/frontend-guide", includeContent: true })`; inspect `#setup-https-on-localhost`. |
| `sd-037` | `curl -LsS https://raw.githubusercontent.com/stellar/stellar-protocol/master/README.md` | `curl -LsS https://raw.githubusercontent.com/stellar/stellar-protocol/master/limits/README.md` |
| `sls-024` | `for q in 'Scam Flagging System' 'Stellar Pulse' Pactta 'The Blue Marble' ChainCred; do curl -sSG https://stellarlight.xyz/api/projects/search --data-urlencode "q=$q" --data-urlencode limit=10; done` | Inspect `statusBasis`, `statusSourceUrl`, and `deployment` on each exact row. |
| `sls-029` | `curl -sS 'https://stellarlight.xyz/api/projects/search?q=oracle&limit=100'` | Inspect `products`, `deployment`, and every evidence field with the OpenAPI descriptions. |
| `sls-033` | `curl -sS 'https://stellarlight.xyz/api/projects/search?type=Wallet&limit=100&offset=0'` | Inspect `types`, `canonicalSlug`, `productKind`, and `availability` with the OpenAPI descriptions. |

## Active record table

GitHub shorthand below means `https://github.com/<owner>/<repo>#<number>`.

### Lumenloop

| ID | Lifecycle | Owner and durable ref | Current state and latest substantive comment | Priority and next action |
|---|---|---|---|---|
| `ll-001` | reported | `lumenloop/lumenloop-backend#21` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-002` | reported | `lumenloop/lumenloop-backend#22` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-003` | reported | `lumenloop/lumenloop-backend#23` | Open. Registered probe recurred. Only comment is by `kalepail` on 2026-07-13. | P2. Keep the local recurrence. |
| `ll-004` | reported | `lumenloop/lumenloop-backend#42` | Open. Latest comment is by `kalepail` on 2026-07-27. | P3. Quiet open issue. |
| `ll-005` | reported | `lumenloop/lumenloop-backend#19` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-006` | reported | `lumenloop/lumenloop-backend#18` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-007` | reported | `lumenloop/lumenloop-backend#20` | Open. Registered probe recurred. Only comment is by `kalepail` on 2026-07-13. | P2. Keep the local recurrence. |
| `ll-008` | reported | `lumenloop/stellar-ecosystem-db#3` | Open. Latest substantive comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. Recheck only after owner activity. |
| `ll-009` | reported | `lumenloop/lumenloop-backend#25` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-010` | reported | `lumenloop/lumenloop-backend#27` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-011` | reported | `lumenloop/lumenloop-backend#24` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-012` | reported | `lumenloop/lumenloop-backend#29` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-013` | reported | `lumenloop/lumenloop-backend#26` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-014` | reported | `lumenloop/lumenloop-backend#30` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-015` | reported | `lumenloop/lumenloop-backend#28` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-016` | reported | `lumenloop/lumenloop-backend#31` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-017` | reported | `lumenloop/lumenloop-backend#36` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-018` | reported | `lumenloop/lumenloop-backend#34` | Open. Latest comment is by `kalepail` on 2026-08-11. | P2. Material recurrence is already recorded. |
| `ll-019` | reported | `lumenloop/lumenloop-backend#35` | Open. Latest comment is by `kalepail` on 2026-08-19. Shares only the schema tracker with `ll-029`. | P3. Keep the A/V date semantics distinct. |
| `ll-020` | reported | `lumenloop/lumenloop-backend#32` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-022` | reported | `lumenloop/lumenloop-backend#38` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-023` | reported | `lumenloop/lumenloop-backend#39` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-024` | reported | `lumenloop/lumenloop-backend#33` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-025` | reported | `lumenloop/lumenloop-backend#37` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-026` | reported | `lumenloop/lumenloop-backend#40` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-027` | reported | `lumenloop/lumenloop-backend#41` | Open. Only comment is by `kalepail` on 2026-07-13. | P3. Quiet open issue. |
| `ll-028` | reported | `lumenloop/lumenloop-backend#43` | Open. No comment. | P3. Quiet open issue. |
| `ll-029` | reported | `lumenloop/lumenloop-backend#35`, comment `#issuecomment-5347713582` | Open. Latest comment is by `kalepail` on 2026-08-19. This covers five non-A/V shapes. | P3. Keep separate from `ll-019`. |
| `ll-030` | reported | `lumenloop/lumenloop-backend#44` | Open. No comment. | P3. Quiet open issue. |

### Skills

| ID | Lifecycle | Owner and durable ref | Current state and latest substantive comment | Priority and next action |
|---|---|---|---|---|
| `sk-004` | reported | `lumenloop/lumenloop-skills#1` | Open. No public substantive comment. | P3. Quiet open issue. |
| `sk-005` | reported | `lumenloop/lumenloop-skills#2` | Open. Registered probe recurred. No public substantive comment. | P2. Keep the recurrence locally. |
| `sk-007` | reported | `lumenloop/lumenloop-skills#3` | Open. Registered probe recurred. No public substantive comment. | P2. Keep the recurrence locally. |
| `sk-014` | reported | `OpenZeppelin/openzeppelin-skills#13` | Open. Registered probe recurred. No public substantive comment. | P2. Keep the recurrence locally. |
| `sk-015` | reported | `OpenZeppelin/openzeppelin-skills#14` | Open. Registered probe recurred. No public substantive comment. | P2. Keep the recurrence locally. |
| `sk-019` | reported | `Stellar-Light/stellar-scout#13` | Open. No public substantive comment. | P3. Quiet open issue. |
| `sk-022` | reported | `OpenZeppelin/openzeppelin-skills#16`; related `#14` | Open. Registered probe recurred. No public substantive comment. | P2. Keep the recurrence locally. Do not collapse it into `sk-015`. |

### Stellar Docs and protocol owners

| ID | Lifecycle | Owner and durable ref | Current state and latest substantive comment | Priority and next action |
|---|---|---|---|---|
| `sd-003` | reported | `stellar/stellar-docs#2566`, PR `#2572` merged | Issue open. Latest comment is `kalepail` on 2026-07-27. | P3. Quiet issue. Preserve the crawler residual. |
| `sd-004` | declined | `stellar/stellar-docs#2567`, PR `#2572` merged | Closed completed. Maintainer `ElliotFriend` explained the policy on 2026-07-13. | P3. Valid declined lifecycle. Revisit only with new evidence. |
| `sd-005` | reported | `stellar/stellar-docs#2565` | Open. Latest comment is `kalepail` on 2026-07-27. The earlier maintainer triage accepted only the attribution defect. | P3. Keep the narrowed recommendation. |
| `sd-009` | declined | `stellar/stellar-docs#2575` | Closed `NOT_PLANNED`. `ElliotFriend` gave the placement decision. The closing comment is by `kalepail`. | P3. Valid declined lifecycle. |
| `sd-014` | reported | `stellar/stellar-docs#2611` | Open. Latest substantive comment is by `ElliotFriend` on 2026-07-21. | P3. Quiet enhancement issue. |
| `sd-027` | reported | `stellar/stellar-docs#2700`; PR `#2367` closed without merge | Issue open. Latest issue comment is `kalepail` on 2026-08-05. The recorded PR is now closed, not an active tracker. | P1. Recheck the two live pages before replacing the closed PR reference. |
| `sd-029` | reported | `stellar/stellar-docs#2602` | Open. Latest comment is `kalepail` on 2026-07-27. | P3. Keep the narrowed BACKFILL residual. |
| `sd-032` | reported | `stellar/stellar-docs#2606`; recorded PR `#2410` merged; linked PR `#2810` draft | Issue open. Latest substantive comment is by `ElliotFriend` on 2026-07-21. PR `#2810` is draft, requests `kaankacar`, and has no review. Its listed checks pass. | P2. Watch the draft. Recheck the tutorial only after it merges. |
| `sd-034` | reported | `stellar/stellar-docs#2700`; PR `#2367` closed without merge | Same issue as `sd-027`, but a separate model-selection defect. Latest issue comment is `kalepail` on 2026-08-05. | P1. Do not merge records. Replace the stalled shared tracker path. |
| `sd-035` | reported | `stellar/stellar-docs#2609`; PR `#2659` merged | Issue open. Latest comment is `kalepail` on 2026-07-27. The merged PR is a stopgap. | P3. Wait for the durable v2 migration. |
| `sd-037` | reported | `stellar/stellar-protocol#1981` | Closed `NOT_PLANNED`. Latest comment is stale bot `github-actions` on 2026-08-14. No maintainer decision is visible. The source trigger still reproduces. | P1. Create a successor or reopen path when approved. |
| `sd-040` | reported | `stellar/stellar-docs#2768`; linked PR `#2849` merged | Closed completed. Source is fixed. The original Raven index trigger remains stale at `#xdr-conversions-in-smart-contracts`. | P1. Require source and index convergence before a fixed-upstream review. |
| `sd-041` | reported | `stellar/stellar-docs#2769`; linked PR `#2853` merged | Closed completed. Source is fixed. The original Raven index trigger remains stale at the page root. | P1. Require source and index convergence before a fixed-upstream review. |
| `sd-044` | reported | `stellar/stellar-docs#2772`; linked PR `#2850` open | Issue open. `kaankacar` confirmed the defect. PR `#2850` is clean and has passing checks. `ElliotFriend` gave two factual corrections on 2026-09-14. | P1. Wait for the author to resolve review comments and merge. Then recheck live Docs. |
| `sd-045` | reported | `stellar/stellar-docs#2773`; linked PR `#2851` merged | Closed completed. Source is fixed. The original Raven index trigger remains stale at `#setup-https-on-localhost`. | P1. Require source and index convergence before a fixed-upstream review. |
| `sd-046` | reported | `stellar/stellar-docs#2842`; linked PR `#2844` open | Issue open. `kaankacar` triage confirmed the finding. PR `#2844` is clean with passing checks and no requested changes. | P1. Wait for merge. Then recheck both general pages. |
| `sd-048` | reported | `stellar/stellar-protocol#2010` | Open. No public substantive comment. | P3. Quiet open issue. |
| `sd-050` | reported | `stellar/stellar-docs#2561` | Open. The issue author is `oceans404`. No public substantive comment is present. | P3. Existing upstream issue is a valid dedupe target. |
| `sd-051` | reported | `stellar/stellar-docs#2843`; linked PR `#2845` open | Issue open. The latest substantive triage is by the `kaankacar` bot. PR `#2845` is clean with passing checks and no requested changes. | P1. Wait for merge. Then recheck the history heading and activation date. |
| `sd-052` | reported | `stellar/stellar-cli#2722` | Open. No public substantive comment. | P3. Quiet open issue. |

### Stellar Light and Scout

| ID | Lifecycle | Owner and durable ref | Current state and latest substantive comment | Priority and next action |
|---|---|---|---|---|
| `sls-024` | reported | `Stellar-Light/stellar-scout#9`; `Stellar-Light/stellarlight#494` | Both issues are closed completed. The five exact source-provenance fixtures now have source URLs. Their explicit unknown deployments are correct semantics. | P2. Record scope-limited improvement. Check QCAD, GLOUSD, and population coverage before any lifecycle change. |
| `sls-029` | reported | `Stellar-Light/stellarlight#514`; consolidated `#742` | Both issues are closed completed. `products: null` and unknown deployment are explicit unknown states, not negative or positive claims. | P2. Do not create a successor from null fields alone. Recheck an unsafe positive claim only. |
| `sls-033` | reported | `Stellar-Light/stellarlight#519`; consolidated `#742` | Both issues are closed completed. Null classification and availability fields are explicit uncurated states. | P2. Do not create a successor from null fields alone. Recheck an unsafe classification or duplicate claim only. |
| `sls-039` | declined | `Stellar-Light/stellarlight#522`; PR `#530` merged | Closed completed. Latest substantive comment is `kalepail` accepting provider-hosted history. | P3. Valid declined lifecycle. Revisit only if the provider link fails. |

### Workers AI provider

| ID | Lifecycle | Owner and durable ref | Current state and latest substantive comment | Priority and next action |
|---|---|---|---|---|
| `wai-001` | reported | `cloudflare/ai#634`; PR `#639` open | Issue open. `edenbuilds` posted the proposed fix on 2026-08-15. PR `#639` is open, has `mergeable_state: unstable`, no reviews, and no reported checks. | P1. Wait for review and successful checks. Re-run the local package trigger only after a release. |

## Open pull request review

| Pull request | State | Checks and reviews | Blocker |
|---|---|---|---|
| `cloudflare/ai#639` | Open, `unstable` | No reviews. No reported checks. | Review and CI are missing. |
| `stellar/stellar-docs#2810` | Draft | Security and CodeQL checks pass. No reviews. `kaankacar` is requested. | Draft state. |
| `stellar/stellar-docs#2837` | Open, clean | All listed checks pass. `ElliotFriend` made comment-only reviews. | No approval is recorded. |
| `stellar/stellar-docs#2844` | Open, clean | All listed checks pass. Bot reviews are comment-only. | No approval is recorded. |
| `stellar/stellar-docs#2845` | Open, clean | All listed checks pass. Bot review is comment-only. | No approval is recorded. |
| `stellar/stellar-docs#2850` | Open, clean | All listed checks pass. `ElliotFriend` made a comment-only review. | The author must apply two factual corrections. |

The audit also found PR `#2837` through `sd-027` and `sd-034`. It is not a
durable reference in either finding. PRs `#2844`, `#2845`, `#2849`, `#2850`,
`#2851`, and `#2853` are issue-linked upstream work. The last three merged.
They do not prove a live fix without the direct checks above.

## Intake, duplicates, and lifecycle review

All active records resolve to an owner in `improvements/intake.json`. The
`stellar-docs` service rule is mixed. Each active Docs record has a concrete
per-finding owner. No active record has an unclear intake target.

There are no exact duplicate findings. The shared references are intentional:

- `ll-019` and `ll-029` share `lumenloop/lumenloop-backend#35`, but separate
  A/V date semantics from five other response shapes.
- `sd-027` and `sd-034` share `stellar/stellar-docs#2700`, but retain separate
  LaunchTube migration and smart-account model-selection defects.
- `sk-015` and `sk-022` link to `OpenZeppelin/openzeppelin-skills#14`, but
  `sk-022` has its own issue `#16` for retired derive APIs.
- `sls-029` and `sls-033` used consolidated issue `stellarlight#742`, but the
  oracle and wallet residuals differ.

The following lifecycle evidence is stale or insufficient:

- `sd-027` and `sd-034` describe PR `#2367` as an active candidate. It is now
  closed without merge.
- `sls-024` has a scope-limited source-provenance improvement. Its five exact
  fixtures now have source URLs. Unknown deployment fields are correct.
- `sls-029` and `sls-033` must not use explicit unknown fields as residual
  evidence. Their closed trackers require no successor from this audit.
- `sd-037` remains reported after stale-bot closure. Its direct source trigger
  still reproduces.
- `sd-040`, `sd-041`, and `sd-045` have source fixes but stale production index
  records. Their original triggers still reproduce, so they are not candidates
  for `fixed-upstream` or retirement.

## Coverage and limits

This audit covered all 61 active files, all durable issue and PR references,
current issue state, latest substantive comments, and all open linked PR
checks and reviews. It used no paid calls and made no external write.

The coordinator supplied the live lint result and the seven registered probe
results. I did not rerun either global command. I directly rechecked seven
closed or changed candidates. The three Docs checks covered both rendered
source and the original production index. I did not rerun the original trigger
for the other 54 records.

Authenticated `gh api` covered all 27 distinct
`lumenloop/lumenloop-backend` issues. All Lumenloop references are current.
Any future lifecycle change still needs its original trigger recheck.
