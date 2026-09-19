# Independent audit review — 2026-09-14

Bounded independent review of two root claims.
No golden edits besides the requested table-label fix.
No register edits. No commits. No paid calls. No new agents.

Reviewed:

- `research/audits/2026-09-14-docs-index-recheck.md`
- `.agents/rounds/2026-09-14-truth-maintenance.md`
- `research/audits/2026-09-14-golden-freshness-review.md` table label only

## Verdicts

1. Direct HTML now agrees with the root: the three rendered pages carry the corrections.
2. Production Raven still returns the original defective text for all three pages.
3. The source-fixed / index-stale split holds on current direct evidence.
4. An earlier web pattern search returned stale page text. That search is not a live-site refutation.
5. Keep `sd-040`, `sd-041`, and `sd-045` unresolved until the serving index drops the defective text.
6. The four symmetric-caution warnings are lint false positives against resolved receipts. Do not restore expired cautions.

## Docs index recheck

Independent production call: Raven `stellarDocs.get_doc_page_sections({path, includeContent:true})` at `2026-09-14T21:20:42.725Z`.
The script returned only booleans, section counts, and ≤140-character excerpts.
It did not return full page payloads.

All three calls returned `ok:true` and `complete:true`.
Section counts match the root table: 7, 15, and 35.

| Finding | Path | Index stale? | Index fixed? | Index excerpt (clipped) |
|---|---|---|---|---|
| `sd-040` | `/docs/build/guides/conversions/address-conversions` | Yes: `.unwrap()` present | No `ConversionError` | `amp;env, &amp;bytes).unwrap()}` |
| `sd-041` | `/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos` | Yes: past-tense lead present | No “still rely on transaction memos” | `We used memos in the past for this purpose, however, using muxed accounts is better` |
| `sd-045` | `/docs/build/guides/dapps/frontend-guide` | Yes: unqualified HTTPS sentence present | No `http://localhost` or `http://127.0.0.1` | `Freighter wallet requires a secure connection (HTTPS) to interact with your dapp.` |

The exact unescaped `Address::from_xdr(&env, &bytes).unwrap()` needle missed because the index stores HTML entities.
The `.unwrap()` hit still proves the original defective call.

### Rendered HTML: earlier search versus direct fetch

Two retrievals must stay distinct.

**Earlier observation (~21:20Z).** A web pattern-search tool reported the old `sd-041` lead and the old `sd-045` HTTPS sentence. That tool can serve a stale fetched page. It is not a direct HTTP GET. It does not refute the root.

**Current direct HTML (2026-09-14T21:27:10Z).** A shell HTTPS GET of the two live URLs returned HTTP 200. Booleans match the root Node fetch at `2026-09-14T21:26:39Z`.

| Finding | Direct HTML 21:27:10Z | Root Node 21:26:39Z |
|---|---|---|
| `sd-041` oldMemo `We used memos in the past for this purpose` | false | false |
| `sd-041` `many services still rely` | true | true |
| `sd-041` `Transaction memos were traditionally used` | true | (not stated) |
| `sd-045` oldHttps `…secure connection (HTTPS) to interact with your dapp.` | false | false |
| `sd-045` `http://localhost` | true | true |
| `sd-045` `http://127.0.0.1` | true | true |

`sd-040` rendered HTML already showed the fallible `ConversionError` example in the earlier pattern search. Direct HTML was not repeated for that page.

GitHub `main` still matches these corrections. PRs `#2849`, `#2853`, and `#2851` remain merged.

| Finding | GitHub `main` | Direct rendered HTML | Production index 21:20:42Z |
|---|---|---|---|
| `sd-040` | Fixed | Fixed (earlier rendered search) | Stale unwrap remains |
| `sd-041` | Fixed | Fixed (direct GET) | Stale past-tense lead remains |
| `sd-045` | Fixed | Fixed (direct GET) | Stale unqualified HTTPS remains |

The root source-fixed / index-stale conclusion stands on this direct evidence.

### Required next check

Do not close these findings yet.

1. Repeat the original production `get_doc_page_sections` queries after ingestion.
2. Confirm each serving index drops the defective text and holds the correction.
3. A merged PR, a GitHub blob, a rendered-page fetch, or a title-count change is not ingestion.

## Symmetric-caution warnings

The ledger says four warnings cite resolved receipts and need lint review.
Independent check confirms that claim.

Lint source: `eval/qa/lint-corpus.mjs` lines 531–534.
It flags any `improvements/` string in `truth.verified.rootCause` when `golden.notes` lacks the three-part caution regex.
It does not distinguish `improvements/resolved.json` from an active finding.

The four warnings from `/tmp/stellar-raven-drift-141-audit-20260914.BHXXv3/repo/evidence/eval-qa-lint.log`:

| Case | rootCause receipts | Receipt state | Notes / evidence |
|---|---|---|---|
| `q-infra-horizon-vs-rpc` | `sd-042` | `improvements/resolved.json`, resolved 2026-09-09 | Notes: “The pre-deploy search-index caution expired after the completed crawl.” |
| `q-protocol-bn254-poseidon-xray` | `sd-021`, `sd-036` | resolved 2026-07-27 and 2026-09-01 | Evidence: “The former CAP-0075 interface contradictions are fixed.” Notes have no live source-conflict caution |
| `q-protocol-ledger-close-time` | `sd-047` | resolved 2026-09-09 | Evidence: “The former source/index conflict no longer applies.” |
| `q-ti-openzeppelin-relayer` | `sd-039` | resolved 2026-09-09 | Notes: “The old product-alias source caution no longer applies.” |

None of these IDs appear in `improvements/INDEX.md`.
They are terminal receipts, not active source conflicts.

Control: `q-pc-practical-fee-setting` also cites resolved `sd-042`.
It still carries a live `sd-003` caution, so the lint stays quiet.
The lint therefore tracks the notes regex, not whether the cited finding is still active.

Restoring expired cautions would punish now-true canonical wording.
Do not restore them to silence the warnings.
Repair the lint so resolved receipts do not require a current caution.

## Golden table label

The freshness report table header `Due now?` was wrong.
October 8 has not happened.
The header is now `Within next 28 days?`.
Past-trigger `lastChecked` dates sit in their own column.
They are completed checks, not overdue evidence.

## Limits

- This pass did not dump full Docs payloads.
- Index name was not present on the projected execute result.
- The production index probe was not re-run after the 21:27Z HTML fetch. The 21:20:42Z index booleans remain the current index evidence.
- The earlier web pattern search is retained only as a stale-tool observation. Direct GET is the live rendered evidence.
- No crawler, index, or finding record was changed.
