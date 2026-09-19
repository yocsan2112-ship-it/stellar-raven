# Live drift issue #141 review — 2026-09-14

## Verdict

**Do not accept the combined candidate.**

The drift is not a mechanical update.
It adds one exposed operation and changes routing text and schemas.
It also changes model-visible skill content and Docs title vocabulary.

The routing gate rejects only the changed manifest fingerprint.
That gate result does not remove the measured numerical regressions.
The candidate loses legacy, extended, and skills grades against the accepted base.

The original RWA enum defect no longer reproduces.
Scout `1.9.51` includes `issued-single-holder` in both state enums.
The live handler also accepts and returns that state.

The original RWA routing blocker still reproduces.
`scout.getRwaAssets` appears in 51 of 495 primary routing lists.
It ranks first in 11 of those lists.
The holdout report adds nine top-five capture rows.
The combined reported total is 60 top-five rows.

The candidate also fails 13 of 2,059 unit tests.
All 94 candidate smoke tests pass.
No repair, acceptance, or baseline change occurred.

## Scope and authority

This review used the repository `live-drift-resolution` skill.
I read `PLAN.md` and `ARCHITECTURE.md` before regeneration.
I also read the current issue and its latest comment.

The latest evidence is [comment 5660180618](https://github.com/stellar-experimental/stellar-raven/issues/141#issuecomment-5660180618).
The older issue body does not describe the complete September 14 drift.
The latest comment points to [workflow run 34815420034](https://github.com/stellar-experimental/stellar-raven/actions/runs/34815420034).

The review was read-only for the primary tree.
I made no commit, deployment, GitHub write, policy change, pin acceptance, or golden change.
I made no generated change in the primary tree.
I did not spawn another agent.

## Candidate identity and environment

| Item | Value |
| --- | --- |
| Primary and clone base | `da4edefebb5d48929ef587356517f9da090a9a2c` |
| Candidate clone | `/private/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/repo` |
| Baseline worktree | `/private/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/baseline` |
| Candidate evidence | `/private/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/repo/evidence` |
| Git | `2.50.1 (Apple Git-155)` |
| Node.js | `v24.13.0` |
| npm | `11.11.0` |
| Vitest | `4.1.11` |
| Wrangler | `4.124.0` |
| Accepted Scout OpenAPI | `1.9.1` |
| Candidate Scout OpenAPI | `1.9.51` |

The result stamps below identify each compared run.

| Result | Stamp or time |
| --- | --- |
| Coordinator accepted routing result | `2026-09-14T21-07-05-843Z` |
| Candidate routing result file | `routing-2026-09-14T21-10-10-160Z.json` |
| Candidate routing `ranAt` | `2026-09-14T21:10:10.161Z` |
| Local accepted-base confirmation file | `routing-2026-09-14T21-10-33-224Z.json` |
| Local accepted-base confirmation `ranAt` | `2026-09-14T21:10:33.225Z` |
| Candidate unit-test start | `2026-09-14T21:13:37.310Z` |
| Candidate smoke-test start | `2026-09-14T21:14:18.212Z` |
| Production skill-health check | `2026-09-14T21:07:17.012Z` |

The clone came from `https://github.com/stellar-experimental/stellar-raven.git`.
Its `package-lock.json` SHA-256 matched the primary file.
Both hashes were `cc2158816188d52686358f25b1c7e8294b940b58c5fceee09660f9f78efb7474`.

The clone used a symlink to the primary `node_modules` directory.
I copied the public skill cache into the clone.
I did not change the September 9 `node_modules/node_modules` self-symlink.

## Exact regeneration commands

These commands ran from the candidate clone unless a path says otherwise.
The `.env` command exported existing values without printing them.

```bash
git clone https://github.com/stellar-experimental/stellar-raven.git /private/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/repo
shasum -a 256 package-lock.json /Users/kalepail/Desktop/stellar-raven-codemode/package-lock.json
ln -s /Users/kalepail/Desktop/stellar-raven-codemode/node_modules node_modules
mkdir -p evidence ecosystem-skills/.cache
cp -R /Users/kalepail/Desktop/stellar-raven-codemode/ecosystem-skills/.cache/. ecosystem-skills/.cache/

set -o pipefail
set -a
. /Users/kalepail/Desktop/stellar-raven-codemode/.env
set +a
node scripts/refresh-inventory.mjs 2>&1 | tee evidence/refresh.log

./ecosystem-skills/update.sh 2>&1 | tee evidence/skills-update.log
node scripts/check-mirrors.mjs --fetch 2>&1 | tee evidence/check-mirrors.log
node scripts/check-pin-review.mjs --base HEAD 2>&1 | tee evidence/check-pin-review.log
node scripts/check-skills-drift.mjs 2>&1 | tee evidence/check-skills-drift.log

node scripts/build-catalog.mjs
npm run micro-map:build
npm run spec:build
node eval/plan/build-op-classes.mjs
node scripts/summarize-live-drift.mjs

npm run eval:compile
npm run eval:routing -- --gate
npm run eval:qa:lint
GIT_CONFIG_COUNT=1 GIT_CONFIG_KEY_0=commit.gpgsign GIT_CONFIG_VALUE_0=false npm test -- --reporter=json --outputFile=evidence/vitest.json
npm run test:smoke -- --reporter=json --outputFile=evidence/smoke-vitest.json
WRANGLER_LOG_PATH=/private/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/repo/evidence/wrangler.log npm run build
npm run secrets:scan -- --tree
git diff --check

npm run algolia:rule-canary -- --require-env --env-file /Users/kalepail/Desktop/stellar-raven-codemode/.env
curl -sS https://raven.stellar.org/health/skills | jq '.'
```

I also ran two direct Scout probes.

```bash
curl -sS https://stellarlight.xyz/api/openapi.json
curl -sS 'https://stellarlight.xyz/api/rwa?state=issued-single-holder&limit=1'
```

The evidence directory contains projected probe results.
It does not contain secret values.

## Regeneration result

The refresh produced these results.

- Lumenloop stayed unchanged after ignoring `fetchedAt`.
- Docs settings stayed unchanged.
- Docs titles changed from 650 to 651.
- Scout changed from 37 to 38 upstream operations.
- Scout changed from OpenAPI `1.9.1` to `1.9.51`.
- The stellar-light skill pin changed.

The full candidate changes nine tracked files.

```text
catalog/manifest.json              | 5236 +++++++++++++++++++++++++++------
ecosystem-skills/INDEX.md          |    8 +-
ecosystem-skills/MANIFEST.json     |   16 +-
ecosystem-skills/catalog.json      |    2 +-
eval/plan/op-classes.json          |    1 +
inventory/stellar-docs-titles.json |    8 +-
inventory/stellar-light.json       | 5662 +++++++++++++++++++++++++++---------
specs/super-spec.json              |  836 ++----
src/mcp/micro-map.ts               |    2 +-
9 files changed, 8976 insertions(+), 2795 deletions(-)
```

`git diff --check` passed.
No hand-authored candidate repair appears in this diff.

## Full drift classification

### Lumenloop

This service has provenance-only stability.
The refresh retained `fetchedAt` because the full inventory stayed unchanged.
Its tool objects, OpenAPI paths, and components stayed unchanged.

### Stellar Docs

This change is routing-relevant data drift.
The title set adds one page and removes no page.

- Title: `Public Dashboards`
- Path: `/docs/data/analytics/public-dashboards`

The title snapshot feeds catalog keywords.
The Algolia settings snapshot stayed unchanged.

### Scout operation surface

This change is operation-surface drift.
It adds `GET /api/rwa` as `scout.getRwaAssets`.
It removes no operation and renames no operation.

The unchanged exposure data automatically emits the new operation.
That result is not an exposure decision.
ADR-0003 requires an explicit decision before acceptance.

### Scout full operation objects

The old inventory has 37 operations.
The candidate has 38 operations.
Thirty existing operation objects change.
Seven existing operation objects remain identical.

The 18 routing-text changes are below.
The listed fields are the changed top-level operation fields.

| Operation | Changed fields |
| --- | --- |
| `scout.analyzeEcosystem` | `responses`, `x-routing` |
| `scout.listAudits` | `x-routing` |
| `scout.getBuilders` | `responses`, `x-routing` |
| `scout.getChangelog` | `responses`, `x-routing` |
| `scout.getChanges` | `responses`, `x-routing` |
| `scout.getClusters` | `x-routing` |
| `scout.listContracts` | `parameters`, `responses`, `x-routing` |
| `scout.getLeaderboard` | `description`, `parameters`, `responses`, `x-routing` |
| `scout.getPartners` | `description`, `parameters`, `x-routing` |
| `scout.matchPartners` | `responses`, `x-routing` |
| `scout.getPartner` | `responses`, `x-routing` |
| `scout.resolveProject` | `x-routing` |
| `scout.searchProjects` | `description`, `parameters`, `x-routing` |
| `scout.getQualityReport` | `description`, `responses`, `summary`, `x-routing` |
| `scout.explainRepo` | `description`, `responses`, `x-routing` |
| `scout.searchRepos` | `x-routing` |
| `scout.searchResearch` | `x-routing` |
| `scout.getRfps` | `description`, `responses`, `x-routing` |

`scout.getQualityReport` remains excluded.
The other 17 routing-text changes affect exposed operations.

The 12 schema-only operation changes are below.

| Operation | Changed fields | Exposure |
| --- | --- | --- |
| `scout.getFeedbackSchema` | `responses` | Excluded |
| `scout.hackathonBrief` | `responses` | Exposed |
| `scout.searchHackathonBuilds` | `responses` | Exposed |
| `scout.compareHackathons` | `responses` | Exposed |
| `scout.partnerAssistant` | `responses` | Excluded |
| `scout.partnerOnboard` | `responses` | Excluded |
| `scout.submitPartnerListing` | `requestBody` | Excluded |
| `scout.getRepoTrust` | `responses` | Exposed |
| `scout.scfPitch` | `responses` | Exposed |
| `scout.getSkill` | `responses` | Exposed |
| `scout.verifyClaim` | `responses` | Excluded |
| `scout.vetIdea` | `responses` | Exposed |

The seven identical objects are below.

- `scout.submitFeedback`
- `scout.getHackathons`
- `scout.getHackathon`
- `scout.getPeople`
- `scout.listSkills`
- `scout.getStablecoins`
- `scout.getStatus`

The complete `openapi.paths` objects are not identical.
This result prevents a provenance-only classification.

### Scout components

The complete `openapi.components` objects are not identical.
Nine shared schemas change.

- `Builder`
- `HackathonDetailResponse`
- `LeaderboardProject`
- `Meta`
- `Partner`
- `PartnersResponse`
- `Project`
- `Repo`
- `Stablecoin`

These schemas can affect several operations.
The candidate super-spec exposes the reachable effects to model code.

### Runner intersection

The runner intersection is empty.
The only runnable skill declares three Lumenloop operations.
No changed Scout operation or component enters that runner.
The skill requires no live runner smoke for this drift.

### Skill pin drift

The candidate changes only the stellar-light source selection.

| Item | Accepted | Candidate |
| --- | --- | --- |
| Commit | `d25b9f6bd842159b5a33aa6125ecb62373c2d8b5` | `3b587aa9f23d21fc572f6e93cb6d11031dbc24e6` |
| Selection digest | `sel:56a2798fd09a` | `sel:339145ff9f53` |
| `SKILL.md` blob | `54f214d228b665bd1f0579ed79dd39226dd9621e` | `de459e784e9e927f42662aa53ab22c8dedab04b7` |
| `api-reference.md` blob | `14f9c9c817ff853089e42333e35a7d60ca7a258a` | `5035cc98f1e0a7339ab9837e2dee19e7da0616cb` |

I read the complete changed-line diff from `ecosystem-skills/update.sh`.
The main skill adds correct SCF-window caution and broader repository-score provenance.
The API reference adds five material contract clarifications.

- Unknown hackathon submissions use `null`, not zero.
- Curated repo search has derived facts that stored rows omit.
- Both repo views expose resolution fields.
- Partner filters add `asset-issuer` and explicit `accepting=0` behavior.
- The reference adds the complete `GET /api/rwa` contract.

The changes add no paid or side-effecting instruction.
The RWA section is still model-visible prompt input.
It must follow the same exposure decision as the operation.

`node scripts/check-mirrors.mjs --fetch` verified all 44 files.
`node scripts/check-skills-drift.mjs` found no later upstream movement.

`node scripts/check-pin-review.mjs --base HEAD` failed as expected.
The ledger lacks a new entry for `stellar-light 3b587aa9f23d sel:339145ff9f53`.
I did not add that entry.
Therefore, this review does not accept the pin.

## Generated runtime impact

The candidate manifest has 254 entries.
It has 61 exposed service operations.

- Lumenloop: 18 operations.
- Scout: 31 operations.
- Stellar Docs: 12 operations.
- Skills: 19 whole skills and 174 sections.

`scout.getRwaAssets` becomes callable through the generic Scout adapter.
The manifest includes its full input and output schemas.
The super-spec adds `/scout/getRwaAssets`.

The super-spec has 65 callable paths, including four skill paths.
It compacts 26 Scout response schemas.
It prunes 21 unreachable components.
Its compact size is 174,278 bytes, or about 43,570 tokens.

The micro-map changes only the Scout count from 30 to 31.
The operation classes add `scout.getRwaAssets` as `detail`.
The total becomes 61 operations: 43 broad, 12 detail, and 6 meta.

The generic runtime wiring works under the smoke tests.
That result does not approve the new operation.
The static Playground sample becomes stale under the changed catalog.

The skill pin would change future `codemode.skill.read` content after deployment.
The skill body does not ship before a deployment.
Current production health therefore does not prove candidate content acceptance.

## Original blockers and current reproduction

| Original blocker | September 14 result |
| --- | --- |
| RWA request enum omitted `issued-single-holder` | Fixed in live OpenAPI `1.9.51` |
| RWA response enum omitted `issued-single-holder` | Fixed in live OpenAPI `1.9.51` |
| The live handler accepted the omitted state | It still accepts the state, now consistently |
| RWA caused broad unrelated routing captures | Still reproduces |
| RWA lacked an explicit ADR-0003 exposure decision | Still reproduces |
| Frozen tests expected 60 operations | Still reproduces with 13 failures |
| Changed pin lacked a current ledger attestation | Still blocks acceptance by design |

The live OpenAPI lists the same four values in both state enums.

```text
live
issued-single-holder
deployed-no-supply
not-found
```

The direct handler probe returned one requested row.
Its state was `issued-single-holder`.
The response reported 34 matching rows.
The registry reported 113 rows across 52 issuers.

This confirms the upstream fix from [Stellar-Light/stellarlight#1529](https://github.com/Stellar-Light/stellarlight/issues/1529).
The fix landed through [Stellar-Light/stellarlight#1532](https://github.com/Stellar-Light/stellarlight/pull/1532).
Raven tracked that retirement in [issue #144](https://github.com/stellar-experimental/stellar-raven/issues/144).

Related retired checks remain in [issue #145](https://github.com/stellar-experimental/stellar-raven/issues/145) and [issue #146](https://github.com/stellar-experimental/stellar-raven/issues/146).
Those upstream fixes do not approve Raven source adoption.

## Routing gate and numerical changes

The accepted baseline re-run passed its gate.
It reproduced the coordinator's accepted counts.
The candidate gate printed one failure reason.

```text
GATE FAIL:
  - catalog/manifest.json SHA-256 does not match the committed gate evidence — re-baseline gates.json explicitly
```

Thus, the gate rejection is fingerprint-only.
The candidate still has real numerical changes against the accepted base.

| Lane | Accepted base | Candidate | Change |
| --- | --- | --- | --- |
| Legacy strict top-1/top-3/top-5 | `213/279/312` | `211/278/312` | `-2/-1/0` |
| Legacy card hits | `95/182` | `103/182` | `+8` |
| Legacy accept-either top-1/top-3/top-5 | `256/317/333` | `259/321/334` | `+3/+4/+1` |
| Extended strict top-1/top-3/top-5 | `90/110/116` | `88/109/114` | `-2/-1/-2` |
| Extended accept-either top-1/top-3/top-5 | `105/118/122` | `105/118/122` | `0/0/0` |
| Skills top-1/top-3/top-5 | `16/23/23` | `16/22/23` | `0/-1/0` |
| Holdout top-1/top-3/top-5 | `10/22/26` | `11/23/27` | `+1/+1/+1` |
| Holdout forbidden/passed | `11/21` | `10/23` | `-1/+2` |
| Protocol positives top-five | `4/8` | `7/8` | `+3` |
| Protocol control captures | `2/4` | `3/4` | `+1` |

The protocol diagnostic still fails.
The candidate improves several accepted-any and holdout measures.
Those gains do not cancel the strict losses.

### Exact per-case losses

The table lists each Boolean grade loss.
It also lists one unchanged-pass rank loss.

| Lane | Case | Loss |
| --- | --- | --- |
| Legacy | `q-comp-yieldblox-oracle-incident` | strict top-1 |
| Legacy | `q-defi-rwa-overview` | strict top-3 |
| Legacy | `q-defi-rwa-scf-similar` | strict top-3 and card hit |
| Legacy | `q-eco-2025-defi-launches` | strict top-5 and card hit |
| Legacy | `q-protocol-24-whisk-incident` | strict top-1, top-3, and top-5 |
| Legacy | `q-protocol-network-passphrases-list` | strict top-3 |
| Legacy | `q-protocol-parallel-execution` | strict top-3 |
| Legacy | `q-protocol-version-history-list` | strict top-1 |
| Legacy | `q-soroban-reentrancy` | card hit |
| Legacy | `q-soroban-sac-balance-storage` | strict top-1 |
| Extended | `q-aas-issuer-fees-supply-cap-freeze` | strict top-1 |
| Extended | `q-defi-build-staking-for-own-token` | strict top-3 and top-5 |
| Extended | `q-pc-account-merge-reclaim-reserve` | strict top-5 |
| Extended | `q-ti-fetch-all-balances-classic-sac` | strict top-1 |
| Skills | `q-skill-soroban-first-contract` | strict top-3 |
| Holdout | `q-holdout-c-04-rwa-digest` | expected rank 2 becomes 3; pass unchanged |

The holdout lane has no Boolean grade loss.
The full hit lists are in `evidence/routing-case-outcomes.json`.

### RWA capture evidence

The primary 495 lists contain these top-five captures.

| Lane | Top-1 | Top-3 | Top-5 |
| --- | ---: | ---: | ---: |
| Legacy, 338 | 8 | 22 | 38 |
| Extended, 122 | 3 | 5 | 11 |
| Skills, 23 | 0 | 0 | 2 |
| Protocol, 12 | 0 | 0 | 0 |
| Total, 495 | 11 | 27 | 51 |

The holdout report adds 2 top-1, 7 top-3, and 9 top-5 capture rows.
These are report rows, not necessarily unique questions.

The historical candidate had 52 of 495 primary captures.
The current candidate reduces that count by one.
It does not resolve the blocker.

Unrelated captures still include the following cases.

- `q-soroban-wasm-size-limit`: rank 1.
- `q-soroban-sac-balance-storage`: rank 1.
- `q-infra-friendbot-fund-testnet`: rank 4.
- `q-infra-what-is-stellar-rpc`: rank 2.
- `q-infra-simulate-transaction-howto`: rank 3.
- `q-ti-fetch-all-balances-classic-sac`: rank 1.
- `q-aas-issuer-fees-supply-cap-freeze`: rank 1.

This result still fails the RWA acceptance rule in `.agents/TODO.md`.
The rule rejects Friendbot, RPC, WASM, simulation, and balance captures.

## Guard and test results

| Check | Result |
| --- | --- |
| `node scripts/refresh-inventory.mjs` | Pass; Scout 38 ops, Docs 651 titles, Lumenloop unchanged |
| `node scripts/build-catalog.mjs` | Pass; 254 entries and 61 service operations |
| `npm run micro-map:build` | Pass; Scout count changes to 31 |
| `npm run spec:build` | Pass; 65 callable paths |
| `node eval/plan/build-op-classes.mjs` | Pass; 61 classes |
| `node scripts/check-mirrors.mjs --fetch` | Pass; 44 files verified from upstream |
| `node scripts/check-skills-drift.mjs` | Pass; all candidate pins match upstream |
| `node scripts/check-pin-review.mjs --base HEAD` | Expected fail; new stellar-light selection has no ledger entry |
| `npm run eval:routing -- --gate` | Fail only on the manifest fingerprint |
| `npm run eval:qa:lint` | Pass; 0 errors and 64 warnings |
| `npm test` | Fail; 2,046 passed and 13 failed |
| `npm run test:smoke` | Pass; 94 passed |
| `npm run build` | Pass after setting `WRANGLER_LOG_PATH` inside the clone |
| `npm run secrets:scan -- --tree` | Pass; no leak found |
| `git diff --check` | Pass |
| Algolia rule canary | Pass; 4 named assertions, read-only, `analytics=false` |
| Production skill health | Pass; 42 files checked at `2026-09-14T21:07:17.012Z` |

The coordinator supplied a clean accepted baseline.
That baseline has 2,059 passing unit tests and 94 passing smoke tests.
Its routing stamp is `2026-09-14T21-07-05-843Z`.

The candidate's 13 unit failures divide into five files.
The table preserves each failed fixture name from `evidence/vitest.json`.

| File | Failed fixture | Observed assertion |
| --- | --- | --- |
| `test/catalog.test.ts` | `build-catalog.mjs has the expected entry counts per service/kind` | Scout count `31`, expected `30` |
| `test/catalog.test.ts` | `x-routing ingestion — routingKeywords and routingPhrases fields attaches routingKeywords to exactly the exposed scout ops that publish x-routing` | Length `31`, expected `26` |
| `test/catalog.test.ts` | `x-routing ingestion — routingKeywords and routingPhrases fields preserves bounded positive source phrases only on exposed Scout operations` | Length `31`, expected `26` |
| `test/demo-page.test.ts` | `static example trace is truthful sample hits/scores/total match the live engine on the current catalog` | Generated page omitted the accepted `4 of 20 matches` text |
| `test/plain-operation-harness.test.mjs` | `plain operation eval harness derives exactly the exposed 60-operation manifest surface` | Operation count `61`, expected `60` |
| `test/search.test.ts` | `searchCatalogPage — structural wider candidates reports an absolute gap with tier context when gated order leads a higher score` | Tier `gated`, expected `backfill` |
| `test/search.test.ts` | `searchCatalog — routing quality keeps the accepted GitHub-activity leaderboard intent inside the Scout quota` | Result list differs from the accepted fixture |
| `test/search.test.ts` | `searchCatalog — routing quality keeps the accepted Stellar GitHub-activity leaderboard intent inside the Scout quota` | Result list differs from the accepted fixture |
| `test/search.test.ts` | `searchCatalog — routing quality changes one later Scout slot without changing page facts or scores` | Empty changed-slot list, expected `scout.searchRepos` |
| `test/search.test.ts` | `searchCatalogPage — tier marker + total/truncated keeps page membership, total, and truncated fixed while interleaving` | Total `80`, expected `79` |
| `test/search.test.ts` | `search-hit signature compaction only output blocks over the threshold are compacted; every other op's search signature is byte-identical` | Compacted-operation list differs from the accepted fixture |
| `test/super-spec.test.ts` | `shape and counts has the expected per-service operation counts (exposed ops only, ADR-0003)` | Scout count `31`, expected `30` |
| `test/super-spec.test.ts` | `consistency with the catalog (single source of truth) every cataloged operation id appears as an operationId (spec = manifest)` | Operation count `61`, expected `60` |

The failures include stale counts and material routing assertions.
The stale assertions must not change before the exposure decision.
The routing failures require evaluation, not mechanical expectation updates.

The first unit run hit sandbox listener and GPG restrictions.
The second run used loopback permission and process-local signing disablement.
The JSON result above comes from the second run.

The first build could not write its default Wrangler log.
The retry wrote the log inside the candidate clone and passed.
No deployment command ran.

## Golden and eval impact

The candidate changes no active golden file.
The active battery contains no direct `getRwaAssets` reference.
It also contains no `/api/rwa` or `issued-single-holder` reference.

Two current golden answers already match the new skill cautions.

- `q-scf-open-rfps-live` distinguishes an open brief from an open submission window.
- `q-scf-hackathon-compare-live` distinguishes unknown submission counts from zero.

No golden truth change is required for those two facts.
The QA lint found zero errors.

The candidate does change the plain-operation QA surface from 60 to 61.
The harness rejects that change before any behavioral QA run.
This failure protects the frozen source epoch.

The routing corpus provides direct RWA impact evidence.
It contains both relevant RWA questions and unrelated implementation questions.
The candidate does not meet the current acceptance checks.

The resolved `sls-082`, `sls-083`, and `sls-084` records remain correct.
They record upstream fixes, not Raven source acceptance.
No improvement status needs a change from this audit.

## Simplest viable next evaluation

Run one isolated source ablation after the owner authorizes it.
Do not change a gate, corpus label, or scoring rule for this ablation.

1. Start from accepted `da4edefebb5d48929ef587356517f9da090a9a2c`.
2. Refresh only Scout to `1.9.51`.
3. Keep the accepted Docs title snapshot.
4. Keep the accepted stellar-light skill pin.
5. Exclude only `GET /api/rwa` in the evaluation clone.
6. Rebuild the catalog, micro-map, super-spec, and operation classes.
7. Run the unchanged routing gate and exact per-case comparison.
8. Run the 11 general scoring acceptance checks in `.agents/TODO.md`.

This ablation isolates the other Scout `1.9.51` changes.
It tests whether RWA causes the remaining source rejection.
It does not approve the exclusion or complete issue #141.

A later full-surface evaluation must expose RWA again.
That evaluation must pass all 11 general scoring checks.
It must keep Friendbot, RPC, WASM, simulation, and balance cases free from RWA capture.

The Docs title and stellar-light pin need separate evaluations.
Do not combine them with the Scout source decision.

## Required next actions

1. Keep issue #141 open and keep Scout `1.9.1` accepted.
2. Do not accept the current combined generated diff.
3. Ask the owner to authorize the isolated Scout ablation.
4. Evaluate Docs title drift separately against the unchanged source surface.
5. Evaluate the stellar-light pin separately and record a new attestation only after approval.
6. Keep the enum finding retired unless the original live trigger fails again.
7. Do not rebaseline `eval/gates.json` to hide strict losses.
8. Update tests and the Playground sample only after an accepted exposure decision.
9. Require an independent reviewer for any operation-surface acceptance.
10. Commit and deploy only after all required gates pass.
11. Verify production after deployment, then close issue #141 with exact evidence.

## Candidate hashes

These hashes identify the preserved candidate.

| File | SHA-256 |
| --- | --- |
| `catalog/manifest.json` | `4df0402c807bf846ad934453d332c4e96f22df9b81355508355a07d4114c9210` |
| `ecosystem-skills/MANIFEST.json` | `19b4b8035f38983a451652993abf5435f1e98980caad9c5dcde3f189f4e62e21` |
| `inventory/stellar-light.json` | `6c3b109dd88979b07d72148e73d5999d83e5fc2928551b0acbe99bc5c121dbd6` |
| `inventory/stellar-docs-titles.json` | `dbd652f5a5d194a2af0006b03d5ce604458739a22db0e81d7c0b39571643d9a0` |
| `specs/super-spec.json` | `0835091f27b0146fa0fcbf0f0ec183717af569be37dcc8d96d3556e011a7e11a` |
| `eval/plan/op-classes.json` | `0f3b603263daf74e35e0bf0baa5ae8522aa602b764b606ff50c1d2380f0d47eb` |
| `src/mcp/micro-map.ts` | `920e3ba0b8e2b3cb9b1f973d709ea625213bf61fee6c42b8abedee39a44e760f` |
| `evidence/eval-routing-gate.log` | `4ed1bf7f8a26e4b117bf0f706573a90e1ec4329c8ef3bc260dc193c150897fac` |
| `evidence/vitest.json` | `fe3237294337c20af300c7eecfd49239219ca5048ec2ade38ba867e0104c4d86` |
| `evidence/smoke-vitest.json` | `d924f421c5897cfbaa0b02742e03b6fe0188bff7ffd505e0768d613dec33fd4f` |

The builder also printed its internal manifest digest.
That digest is `821a3d516ed4e5f904bcbba134646e6fbe3329f1a57852cbf0f3bfd8b9082092`.
The table uses the complete file SHA-256.

## Preserved evidence

The temporary clone remains available for review.
Important evidence files include the following paths.

- `evidence/refresh.log`
- `evidence/skills-update.log`
- `evidence/check-mirrors.log`
- `evidence/check-pin-review.log`
- `evidence/check-skills-drift.log`
- `evidence/full-operation-component-diff.json`
- `evidence/drift-summary.md`
- `evidence/eval-routing-gate.log`
- `evidence/routing-comparison.json`
- `evidence/routing-case-outcomes.json`
- `evidence/live-rwa-openapi-probe.json`
- `evidence/live-rwa-handler-probe.json`
- `evidence/vitest.json`
- `evidence/smoke-vitest.json`
- `evidence/eval-qa-lint.log`
- `evidence/npm-build-retry.log`
- `evidence/secrets-scan.log`
- `evidence/algolia-rule-canary.log`
- `evidence/production-skills-health.json`

`/private/tmp` is temporary storage.
The evidence remains present now, but the operating system can remove it later.

## Limits

- I did not run a paid operation.
- I did not call the candidate through deployed Raven.
- Direct Scout probes tested the upstream service only.
- Production still serves an accepted compiled surface.
- Production skill health tests the deployed pin, not the candidate pin.
- I did not run `npm run typecheck` in the temporary clone.
- The build and smoke lanes covered generated runtime assembly.
- The unit lane covered 2,059 tests.
- I did not inspect Cloudflare logs.
- I made no GitHub state change.
- I made no crawler, Algolia, or index write.
- I made no pin ledger entry.
- I made no policy, test, gate, or golden edit.
- I preserved unrelated primary-tree files.
