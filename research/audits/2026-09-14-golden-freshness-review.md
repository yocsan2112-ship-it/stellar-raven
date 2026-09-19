# Golden freshness review — 2026-09-14

Read-only audit. No golden edits. No register edits. No commits. No paid tools. No child agents. No external messages.

Observed at: 2026-09-14.
Window: next 28 days through 2026-10-12.
Skill: `.agents/skills/golden-truth/SKILL.md`.

## Method

This pass re-reads the six due case files.
It re-checks important claims from live primary sources.
It uses independent source classes where a free path exists.

Classes used:

| Class | Tools this pass |
|---|---|
| A | Official Docs, SDF pages, Meridian site, Lab Docs |
| B | GitHub `stellar/laboratory`, `stellar/stellar-protocol`, `stellar/x402-stellar`, `stellar/passkey-kit`, `stellar/launchtube`, `script3/yieldblox-incident-remediation`, `DK27ss/YieldBlox-10M-PoC` |
| C | Free Raven `execute` and `search`; Scout `getBuilders`; LumenLoop person lane; Docs index |
| D | Built-in web search and X post fetch only. No Perplexity. No Parallel. No paid LumenLoop research |
| E | Docs index hits through Raven `stellarDocs.search_*` |
| F | Horizon REST effects; local `stellar contract asset --help`; live Lab JS bundle; no signing or submit |

The aggregator never corroborates itself.
Scout `getBuilders` is the closed-world surface for the Strupey miss.
LumenLoop person-lane emptiness is source-scoped retrieval evidence, not an open-world negative.

## Overall hold/edit verdict

Hold all six goldens.
No gospel change is justified on this evidence.
Two date-contingent traps fire on 2026-10-08.
This pass is an early recheck of those traps.
It does not close them.

Source-metadata drift exists.
It is not a live contradiction of the asserted facts.

## Case 1 — `q-ti-stellar-lab-usage-and-new-ui`

- File: `eval/qa/corpus/battery/tooling-infra/q-ti-stellar-lab-usage-and-new-ui.json`
- Domain: mixed. Status: confirmed. Freshness: scheduled.
- `asOf`: 2026-09-09. `reverifyBy`: 2026-10-01.
- Last gospel verification: 2026-09-09 storage correction.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| Current Lab supports network selection, build/sign/simulate/submit, contracts, RPC/Horizon, XDR↔JSON, and saved/shareable work | confirmed-as-of | A, E | https://developers.stellar.org/docs/tools/lab (2026-09-14); https://lab.stellar.org (HTTP 200, 2026-09-14); Docs index hits the Lab feature pages | Docs: “Create Accounts on Mainnet, Testnet, and Futurenet”; “simulate transactions, save transactions, and submit transactions”; XDR to JSON; saved/shareable requests |
| Transaction walkthrough uses Fetch next sequence, add operation, then sign/submit; do not freeze coordinates | confirmed-as-of | A, E | https://developers.stellar.org/docs/tools/lab/transactions (2026-09-14); https://developers.stellar.org/docs/build/agentic-payments/x402/quickstart-guide#using-stellar-lab | “clicking the **Fetch next sequence** button”; “Add Operation”; “Sign in Transaction Signer” |
| Signing paths include wallet, hardware, external, and raw-secret; Saved Keypairs are Testnet/Futurenet only | confirmed-as-of | A, B, F | https://developers.stellar.org/docs/tools/lab/saved/keypairs (2026-09-14); https://developers.stellar.org/docs/tools/lab/smart-contracts/upload-deploy-contract (web search 2026-09-14); live Lab JS 2026-09-14 | Docs: “only Testnet and Futurenet”; “never on Mainnet”. Live UI: “This feature is only available on Futurenet and Testnet for security reasons.” Upload/deploy docs name secret key, hardware wallet, extension wallet, and signature |
| As of 2026-09-09, new Saved Keypairs writes use reversible XOR/base64 obfuscation; legacy plaintext remains readable; this is not secure custody | confirmed-as-of | A, B, F | Docs keypairs page 2026-09-14; GitHub `stellar/laboratory` `src/helpers/jsonCipher.ts` and `localStorageSavedKeypairs.ts` at SHA `bbbe48c79b8a90bbc548115a0573c912b1e9fa9e` (2026-09-14); live bundle `https://lab.stellar.org/_next/static/chunks/app/(sidebar)/account/saved/page-dbc03db5d85268bb.js` (same hash as 2026-09-09) | Docs: “obfuscated, but *not* encrypted”; “keypairs saved before September 2025 may remain in plain text”. Source: `SALT = Networks.TESTNET`; `encryptJson` is XOR then `btoa`; reads try `JSON.parse` first. Live UI: “stored in the browser’s localstorage unencrypted and with no protection” |
| `stellar contract asset deploy` deploys a SAC; `stellar contract id asset` only derives the ID | confirmed | A, B/F, E | https://developers.stellar.org/docs/tools/cli/cookbook/deploy-stellar-asset-contract (2026-09-14); https://developers.stellar.org/docs/tools/cli/stellar-cli; local `stellar contract asset --help` (2026-09-14) | Docs show both commands. CLI help: `id` “Get Id… Deprecated, use `stellar contract id asset` instead”; `deploy` “Deploy builtin Soroban Asset Contract” |
| Friendbot is non-production Testnet/Futurenet funding; a trustline does not credit units | confirmed | A | Lab Docs feature list 2026-09-14; Saved Keypairs page Friendbot note | “Friendbot to fund those accounts directly on Lab for Testnet and Futurenet”; unfunded saved accounts can “get 10,000 XLM” on test networks |
| Self-hosted/local Lab is not automatically offline or air-gapped; Quickstart is not production | confirmed-as-of | A | https://developers.stellar.org/docs/tools/quickstart (2026-09-14) | “not intended for production purposes”. This pass did not re-walk a live Quickstart `/lab` path |
| Dedicated current Lab SAC-creation button | unverifiable | A | Upload/deploy docs describe WASM upload/deploy, not a dedicated SAC button | Golden already forbids inventing that button. No live UI click-through this pass |

### Source-metadata note

The case source list still cites `https://developers.stellar.org/docs/tools/cli/cookbook/contract-assets`.
That URL returned Docs “Page Not Found” on 2026-09-14.
The live cookbook page is `https://developers.stellar.org/docs/tools/cli/cookbook/deploy-stellar-asset-contract`.
The SAC claim remains confirmed.
Replace the dead URL at the next authorized gospel edit.

### Sibling impact

- `q-tool-lab-what-is`: still names `lab.stellar.org` and Testnet/Futurenet Friendbot. No contradiction. Its `reverifyBy` is 2027-01-21.
- `q-ti-secret-key-vs-mnemonic-derivation`: cluster-137 still matches reversible obfuscation plus legacy plaintext. No contradiction.
- cluster-023 Friendbot boundary still matches.

### Required follow-up

1. On or before 2026-10-01, refresh `truth.verified` after a gospel-authorized pass.
2. Replace the dead cookbook URL in `truth.sources`.
3. If UI coordinates or signer labels change, re-open the capability claim with a read-only Lab inspection. Do not sign or submit.
4. Confirm Quickstart `/lab` only if that path is still asserted.

## Case 2 — `q-builder-content-by-person`

- File: `eval/qa/corpus/battery/scf-grants-builders/q-builder-content-by-person.json`
- Domain: mixed. Status: confirmed. Freshness: scheduled.
- `asOf`: 2026-07-13. `reverifyBy`: 2026-10-07.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| Official author index shows Tyler van der Hoeven and seven posts | confirmed-as-of | A | https://developers.stellar.org/meetings/authors/kalepail (2026-09-14) | Page title: “Tyler van der Hoeven - 7 posts” |
| 2024-06-13 meeting covers Super Peach, Passkey Kit, and Launchtube | confirmed | A | https://developers.stellar.org/meetings/2024/06/13 (2026-09-14) | “Tyler created Super Peach”; “Introduced `passkey-kit`”; “Introduced Launchtube”. JSON-LD `datePublished`: 2024-06-13 |
| Practical Path Payments is dated 2020-04-10 and names Tyler | confirmed | A | https://stellar.org/events/community/practical-path-payments (2026-09-14) | “April 10, 2020 at 5.00 PM UTC”; speaker “Tyler van der Hoeven” |
| Turing Complete Contract Proposal page header is 2020-07-10 while body says June 19 | confirmed | A | https://stellar.org/community/events/turing-complete-contract-proposal-for-stellar (2026-09-14) | Header: “July 10, 2020 at 5.00 PM UTC”. Body: “tune in on June 19th 2020, 1:00 PM ET!” Conflict still live |
| SDF Developer Advocates AMA is dated 2023-05-04 and names Tyler | confirmed | A | https://stellar.org/events/community/ama-with-sdfs-new-developer-advocates (2026-09-14) | “May 4, 2023 at 2.00 PM UTC”; speakers include Tyler van der Hoeven |
| `kalepail/passkey-kit` as of 2026-07-13 described a v1 SDK and a non-drop-in Smart Account Kit sibling; the repo later moved | confirmed-as-of | B | https://github.com/kalepail/passkey-kit (archived 2026-07-31, fetched 2026-09-14); https://github.com/stellar/passkey-kit (2026-09-14) | Archived README still has the v1 description and “not drop-in compatible”. Canonical continuation is `stellar/passkey-kit` |
| `stellar/launchtube` remains a directly inspectable source repository | confirmed-as-of | B | https://github.com/stellar/launchtube (2026-09-14) | Repo is public and readable. Owner archived it on 2026-03-09 and marks it legacy. The dated 2026-07-13 inspectability claim still holds |
| Exact LumenLoop person lane is empty; emptiness is not proof of no publication | confirmed-as-of | C, A | Raven `lumenloop.find_content_by_entity(entity=Tyler van der Hoeven, entity_type=person)` 2026-09-14; official author index above | Person collections: articles 0, av 0, events 0, proposals 0, scf_submissions 0. Official sources still publish Tyler content |
| Semantic LumenLoop hits need exact-name validation | confirmed | C | Raven `lumenloop.search_content_semantic(query="Tyler van der Hoeven")` 2026-09-14 | 30 items. Sample includes the AMA page and adjacent VELO/OtterSec rows. Adjacent hits must not be attributed |

### Sibling impact

- `q-builder-justin-rice-history`: still the positive dated-history control. No contradiction.
- `q-edge-lumenloop-person-entity-empty`, `q-gap-semantic-directory-fallback`: person-lane emptiness and semantic-validation caution still match.
- cluster-073 and cluster-128 remain consistent on this evidence.
- `stellar/launchtube` archive is new operational status for later dated rosters. It does not falsify the 2026-07-13 observation.

### Required follow-up

1. On or before 2026-10-07, re-count the author-index posts. Seven is a roster, not a durable invariant.
2. At gospel-edit time, date the Launchtube archive/legacy status if the roster is refreshed.
3. Keep ll-005 / ll-017 grader caution until those findings change.

## Case 3 — `q-comp-yieldblox-oracle-incident`

- File: `eval/qa/corpus/battery/compliance-rwa-payments/q-comp-yieldblox-oracle-incident.json`
- Domain: mixed. Status: mixed. Freshness: scheduled.
- `asOf`: 2026-07-28. `reverifyBy`: 2026-10-08.
- Register trap: dateContingentTraps entry “2026-10-08 YieldBlox/Reflector remediation recheck…”. Disposition remains open. This pass does not close it.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| Drain occurred on 2026-02-22 via thin USTRY SDEX manipulation into Reflector, accepted by the YieldBlox Blend V2 pool | confirmed | B, D, F, C | PoC README 2026-09-14; BlockSec 2026-02-26; Blockaid 2026-05-20; Horizon tx timestamps 2026-02-22; Scout research hit 2026-09-14 | PoC: “Date: February 22, 2026 ~00:25 UTC”. Horizon: USDC tx `2026-02-22T00:22:09Z` ledger 61340384; XLM tx `2026-02-22T00:24:27Z` ledger 61340408. Blockaid: “max_dev = 10”; two consecutive poisoned windows. Scout research still anchors the Blockaid post |
| Exploit transfers were 61,249,278.3064502 XLM and 1,000,196.7040837 USDC | confirmed | F, B, D | Horizon effects 2026-09-14; PoC README; BlockSec borrow table | Horizon USDC amount `1000196.7040837`; XLM amount `61249278.3064502`. PoC and BlockSec name the same two hashes |
| Pre-transaction ~14,000 USDC liability was not a second exploit borrow of 1,014,196.7040837 USDC | contradicted (avoid trap) | B, F | PoC pre-TX1 state 2026-09-14; Horizon shows only the 1,000,196.7040837 USDC effect | PoC: existing “~14,000 USDC” liability; exploit call amount `10001967040837` |
| Script3 later estimated about $10.5M net loss | unverifiable | A/D, B | Script3 X posts 2026-02-23 / 2026-02-27 / 2026-03-20; remediation README 2026-09-14; no accessible operator article | No live Script3 page recovered `$10.5M net loss`. Secondary writeups still use $10.2M / $10.86M / $10.97M. Keep unverifiable |
| About 48M XLM quarantined was recovered attacker money | contradicted (avoid trap) | D, B | Blockaid 2026-09-14; Script3 remediation README | Blockaid: “Approximately 48,069,094 XLM was effectively quarantined”; “prevented from further movement”. No “recovered” wording. README is refund logs, not attacker repayment |
| Script3 supplier remediation 2026-02-27 and backstop remediation 2026-03-20, with exclusions | confirmed | A, B | https://x.com/script3official/status/2027462360294953200 (2026-02-27); https://x.com/script3official/status/2035066332887023761 (2026-03-20); GitHub remediation repo | Feb 27: depositor payments; skips under 0.01; not for liquidations or backstop. Mar 20: backstop distributed; “no remediation for those liquidated”; “concludes Script3’s remediation effort” |
| Staleness caused the incident, or TWAP alone would have prevented it | contradicted (avoid trap) | B, D | PoC poisoned-but-fresh rounds; Blockaid max_dev adjacent-window explanation | Poisoned values were fresh consecutive windows, not stale |

### New-status check for the 2026-10-08 trap

No new official final post-mortem appeared in free sources.
Script3 already called remediation concluded on 2026-03-20.
Blockaid still says validators quarantined funds and that the team is “working to recoup” about $1.7M.
That recoup line is not proof of attacker repayment.
Do not equate quarantine with recovery.

### Sibling impact

- `q-hist-yieldblox-v2-2026-exploit`: same transfers, same 14,000-USDC caution, same unverifiable $10.5M. No contradiction.
- `q-soroban-oracle-defensive-consumption`: still in the date-contingent trap and cluster-126.
- cluster-013 and cluster-126 remain consistent.

### Required follow-up

1. On 2026-10-08, re-run the register trap recheck. Do not close it from this early pass.
2. Re-fetch Script3 notices, the remediation repo, and Blockaid/BlockSec.
3. Keep token quantities pinned only if Horizon/PoC still match.
4. If a primary Script3 net-loss figure appears, encode it as disputed or dated. Do not average it into one loss number.

## Case 4 — `q-hist-meridian-2026-corrected-venue`

- File: `eval/qa/corpus/battery/history-org-tokenomics/q-hist-meridian-2026-corrected-venue.json`
- Domain: real-world. Status: confirmed. Freshness: scheduled.
- `asOf`: 2026-07-11. `reverifyBy`: 2026-10-08.
- Register trap: “2026-10-08 pre-event check and Meridian 2026 on 2026-10-28/2026-10-29”. Disposition remains open.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| Current official schedule is 2026-10-28–29 at Convento do Beato, Lisbon | confirmed-as-of | A | https://meridian.stellar.org/ (2026-09-14); https://meridian.stellar.org/event-details (2026-09-14); https://stellar.org/events (web search 2026-09-14) | Home: “October 28-29.2026 · Convento do Beato, Lisbon, Portugal”. FAQ: “October 28–29, 2026 at Convento do Beato in Lisbon, Portugal” |
| HackMeridian is 2026-10-25–26 in Lisbon | confirmed-as-of | A | https://www.hackmeridian.com/ (2026-09-14); Meridian FAQ | “October 25–26, 2026 · Lisbon, Portugal” |
| SDF announced Lisbon and October 28–29 on 2026-04-01 | confirmed | A | https://x.com/StellarOrg/status/2039405316803031315 timestamp Wed, 01 Apr 2026 18:11:32 GMT | “Meridian is headed to Lisbon. October 28–29.” |
| Abu Dhabi / Yas Marina October 21–22 is the current schedule | contradicted (avoid trap) | A | Official site and April 1 post above | Current pages do not present Abu Dhabi as current |
| Independent listing still points at Lisbon and defers to the official site | confirmed-as-of, with lag | D | https://luma.com/meridian2026ll (2026-09-14) | Title “Meridian 2026 Lisbon”. Body: “placeholder event. See meridian.stellar.org”. It still says “Exact venue to be announced”. Official site now names Convento do Beato. Treat Luma as non-authority |
| Older CoinDesk recap preserves the superseded Abu Dhabi dates | unverifiable this pass | D | https://www.coindesk.com/sponsored-content/what-you-missed-at-the-stellar-meridian-conference | Fetch returned a Vercel security checkpoint. Do not refresh that trap from this pass |

### New operational facts for the 2026-10-08 trap

FAQ: registration closes 2026-10-09, or when sold out.
No on-site ticket sales.
Keep the as-of qualifier while the event remains upcoming.
Do not freeze ticket prices as gospel.

### Sibling impact

- `q-scf-hackathons-active` is live/dated roster, not a venue pin. No contradiction.
- Grep of the battery still finds no other case that pins Abu Dhabi as current.

### Required follow-up

1. On 2026-10-08, re-fetch `meridian.stellar.org` and `event-details`.
2. Confirm registration is still open or closed.
3. After 2026-10-29, convert the current-schedule claim from upcoming to historical, or record cancellation/change.
4. Do not use Luma as venue authority.

## Case 5 — `q-hist-x402-stellar-announcement`

- File: `eval/qa/corpus/battery/history-org-tokenomics/q-hist-x402-stellar-announcement.json`
- Domain: real-world. Status: confirmed. Freshness: scheduled.
- `asOf`: 2026-07-11. `reverifyBy`: 2026-10-08.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| SDF announced x402 on Stellar on 2026-03-10 | confirmed | A, D | https://stellar.org/blog/foundation-news/x402-on-stellar (published 2026-03-10 per web index); https://x.com/StellarOrg/status/2031446354808254563 2026-03-10 19:05 UTC; https://x.com/BuildOnStellar/status/2031446327138345301 | Blog title live. SDF post: “x402 is live on Stellar.” |
| x402 is programmatic per-request HTTP 402 payments on Stellar using Soroban auth and SEP-41 tokens | confirmed | A, B | https://developers.stellar.org/docs/build/agentic-payments/x402 (2026-09-14); https://github.com/stellar/x402-stellar | Docs: “per request payments over HTTP”; “Soroban authorization”; “any SEP-41 compliant token” |
| At announcement, settlement was live and agent/MCP tooling was still being built | confirmed-as-of | A, B | Blog “What's ahead” section 2026-09-14; `stellar/x402-stellar` README 2026-09-14 | Blog still: “The settlement layer is live. The agent tooling is being built.” “MCP integration… is in active development.” Current repo has tools and examples. That does not rewrite the announcement-time boundary |
| x402 had no SEP number as of 2026-07-11, and still has none as of 2026-09-14 | confirmed-as-of | A, B, D | GitHub `stellar/stellar-protocol/ecosystem` listing 2026-09-14: `sep-0001` through `sep-0059`, no `sep-0402`; GitHub code search `x402 repo:stellar/stellar-protocol` total_count 0; search `sep-0402 OR SEP-402` total_count 0; https://developers.stellar.org/docs/learn/fundamentals/stellar-ecosystem-proposals (2026-09-14) active list has no x402 | Negative claim remains source-relative. Free sweep found implementation/docs, not a SEP identity |

### Sibling impact

- cluster-125: announcement date stays historical; current facilitator/wallet status stays separately dated. No contradiction with this case.
- `q-defi-x402-on-stellar-what` (as of 2026-07-10) said the Linux Foundation page still reported an unseated Governing Board. Live https://stellar.org/x402 now says SDF “holds a seat on the Foundation's Governing Board”. That is a sibling freshness issue, not a defect in this announcement case.
- Docs now list Scopuly in addition to the older wallet roster. That roster belongs to implementation cases, not this announcement case.

### Required follow-up

1. On 2026-10-08, re-list `stellar-protocol/ecosystem` for a new SEP.
2. Keep announcement-time tooling status distinct from current demo/repo maturity.
3. Queue a separate golden-truth pass for `q-defi-x402-on-stellar-what` board-seat wording. Do not edit it here.

## Case 6 — `q-edge-closed-world-builder-directory-miss`

- File: `eval/qa/corpus/battery/edge-behavior/q-edge-closed-world-builder-directory-miss.json`
- Domain: corpus-grounded. Status: confirmed. Freshness: scheduled.
- `asOf`: 2026-07-13. `reverifyBy`: 2026-10-09.
- Trap: `fabrication-bait`.

### Corroboration matrix

| Claim | Verdict | Classes | Exact refs and dates | Quote or observation |
|---|---|---|---|---|
| Scout builder directory returned no exact Strupey record on 2026-07-13, and still returns none on 2026-09-14 | confirmed-as-of | C | Raven `scout.getBuilders({ q: "Strupey" })` 2026-09-14T21:10:50.040Z; https://stellarlight.xyz/api/builders?q=Strupey 2026-09-14T21:12:44.601Z | `builders: []`. Live meta: `matchMode=expanded`, `counts.returned=0`, `counts.total=0`. Advisory: “The directory has 183 builder profiles, but none match these filters”. This is a filter miss, not an empty directory |
| The negative is Scout-scoped and dated; it does not prove Strupey has no history elsewhere | confirmed | C, A/B | Same directory miss; paired open-world case `q-edge-strupey-ambiguous-stellar-history` | Live advisory says an empty result is “NOT evidence the person doesn't exist” |
| Do not substitute a semantic neighbor for an exact builder record | confirmed | C | Expanded match still returned zero rows | No neighbor row to mis-attribute on this surface |

### Sibling impact

- `q-edge-strupey-ambiguous-stellar-history`: open-world non-verification remains compatible.
- `q-edge-open-world-recovery-after-narrow-miss` and `q-gap-semantic-directory-fallback`: closed-world vs open-world split still holds.
- cluster-128 remains consistent.
- Sibling `q-gap-builders-person-empty` still says the directory held 114 profiles in its N1 probe. Live advisory now says 183. That roster count is a sibling freshness item. It does not change this miss.

### Required follow-up

1. On or before 2026-10-09, re-probe `scout.getBuilders(q=Strupey)` and the public builders API.
2. If any exact Strupey row appears, this closed-world negative becomes false and needs a gospel change.
3. Report `matchMode`. Expanded zero is still a miss. An expanded non-zero neighbor is not an exact record.

## Consistency-register inspection

Inspected `eval/qa/consistency-register.json`.
No edits.

### Queued traps

There is no `queued` section in the register.
Cluster verdicts in this file are `consistent`.
No `inconsistent` or `queued` cluster verdict was found.
The six due cases have `truth.lifecycle.reviewState: "none"`.
Generated `eval/qa/lifecycle-registry.json` counts: proposed 0, active 500, quarantined 0, retired 0.

### Date-contingent traps vs the 28-day window

Today is 2026-09-14.
The 28-day window ends 2026-10-12.
October 8 has not occurred.
A past `lastChecked` date is a completed check. It is not overdue evidence.

| Trap trigger | Within next 28 days? | Disposition | lastChecked | Cases | This-pass action |
|---|---|---|---|---|---|
| 2026-10-08 YieldBlox/Reflector remediation recheck or final post-mortem/reimbursement | Yes | open | 2026-08-29 | `q-comp-yieldblox-oracle-incident`, `q-hist-yieldblox-v2-2026-exploit`, `q-soroban-oracle-defensive-consumption` | Early recheck. Trigger has not fired. No close. No register change |
| 2026-10-08 pre-event check and Meridian 2026 on 2026-10-28/29 | Yes for 2026-10-08; event dates are outside this window | open | 2026-08-31 | `q-hist-meridian-2026-corrected-venue` | Early recheck. Lisbon/Convento still current. Keep as-of. No register change |
| 2026-08-27 or any earlier Circle CCTP V2 fee/finality/support update | No | open | 2026-08-31 | CCTP cases, not in this six | Past trigger. `lastChecked` 2026-08-31 is a completed check, not overdue evidence. Still open. Do not change |
| SCF #46/#45/#44 phase change after fixed #43 | No; event-triggered | reviewed 2026-09-03 | 2026-09-03 | SCF current-round cases | No dated trigger in this window. Do not change |
| Confidential Tokens Mainnet approval/launch; 2026-11-19/2026-12-15 review | No | open | 2026-09-02 | Confidential-token cases | Outside 28 days |
| Protocol 28 / AddressV2 activation | No; event-triggered | open | 2026-09-03 | protocol-version cases | No dated fire in this window |
| Noether audit clearance or Mainnet perps launch | No; event-triggered | open | 2026-08-27 | `q-defi-perps-whitespace` (`reverifyBy` 2026-10-29) | Outside this six-case set. `lastChecked` 2026-08-27 is a completed check, not overdue evidence |

Do not treat this audit as a register re-stamp.

## Cross-case sibling sweep

Grep and live reads found no pair of goldens that cannot both be true.

| Topic | Cases checked | Result |
|---|---|---|
| Lab storage and Friendbot | `q-ti-stellar-lab-usage-and-new-ui`, `q-tool-lab-what-is`, `q-ti-secret-key-vs-mnemonic-derivation` | Consistent |
| Tyler roster and empty person lane | `q-builder-content-by-person`, `q-builder-justin-rice-history`, `q-edge-lumenloop-person-entity-empty` | Consistent |
| YieldBlox quantities and recovery | `q-comp-yieldblox-oracle-incident`, `q-hist-yieldblox-v2-2026-exploit`, `q-soroban-oracle-defensive-consumption` | Consistent |
| Meridian venue | `q-hist-meridian-2026-corrected-venue`, `q-scf-hackathons-active` | Consistent; live roster is separately dated |
| x402 announcement vs SEP identity | `q-hist-x402-stellar-announcement`, `q-defi-x402-on-stellar-what`, `q-x402-payment-verification` | No contradiction on announcement/SEP. Board-seat wording on the live x402 landing page is a sibling freshness item |
| Strupey closed-world miss | `q-edge-closed-world-builder-directory-miss`, `q-edge-strupey-ambiguous-stellar-history`, `q-edge-open-world-recovery-after-narrow-miss` | Consistent |

## Concrete required follow-up

Do these in a later authorized golden-truth pass. Do not do them in this audit.

1. `q-ti-stellar-lab-usage-and-new-ui` by 2026-10-01: refresh verification; replace dead cookbook URL; optional read-only Lab UI pass.
2. `q-builder-content-by-person` by 2026-10-07: re-count author posts; date Launchtube archive if the roster is rewritten.
3. YieldBlox register trap on 2026-10-08: recheck remediation/recovery; keep mixed status unless primary evidence changes.
4. Meridian register trap on 2026-10-08: re-fetch official venue/dates; note registration close on 2026-10-09; keep as-of until the event completes.
5. `q-hist-x402-stellar-announcement` by 2026-10-08: re-list SEPs; keep no-SEP as dated.
6. `q-edge-closed-world-builder-directory-miss` by 2026-10-09: re-probe builders; if an exact row appears, change gospel.
7. Separate later pass: `q-defi-x402-on-stellar-what` Governing Board seat; `q-gap-builders-person-empty` 114 vs live 183.

## Verification limits

- No paid class D tools. Negative SEP and post-mortem sweeps used GitHub, official docs, built-in web search, and X fetch only.
- CoinDesk stale recap was blocked by a Vercel checkpoint. That older-source trap was not re-walked.
- Stellar Expert HTML needs JavaScript. Transfer amounts come from Horizon REST effects instead.
- Lab saved-keypairs UI is a Next.js app. This pass read Docs, source, and the live JS bundle. It did not click the page in an isolated browser. No keys were written. No transaction was signed or submitted.
- Quickstart `/lab` was not executed locally.
- Script3 X posts were read from search snippets and IDs, not from a logged-in X session beyond the Meridian thread fetch.
- `scout.searchResearch` is candidate discovery for YieldBlox. It is not independent corroboration of Blockaid.
- LumenLoop semantic rows are candidates only.
- Directory `matchMode` was `expanded`, not a documented exact-match mode. Zero rows still support the closed-world miss.
- Local `stellar contract asset --help` confirms command names. It does not deploy a SAC.

## Decision

Hold gospel for all six cases.
Keep both 2026-10-08 date-contingent traps open.
Do not edit goldens, the register, or findings from this file.
