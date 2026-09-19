# Docs source and index recheck — 2026-09-14

## Result

The rendered pages contain corrections for `sd-040`, `sd-041`, and `sd-045`.
The production Raven index still returns the original defective text for all three pages.
Keep these findings unresolved. Source deployment alone does not complete their verification.

## Independent production check

The root used production Raven `execute` at `2026-09-14T21:16:57Z`.
Each call used `stellarDocs.get_doc_page_sections({path, includeContent:true})`.
All three calls returned `ok:true` and `complete:true`.
The configured serving index is `crawler_Stellar Docs - Docusaurus`.

| Finding | Exact path | Sections | Observed defective text | Corrected evidence in these sections |
|---|---|---:|---|---|
| `sd-040` | `/docs/build/guides/conversions/address-conversions` | 7 | `Address::from_xdr(&amp;env, &amp;bytes).unwrap()` | No `ConversionError` |
| `sd-041` | `/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos` | 15 | `We used memos in the past for this purpose` | The original lead remains |
| `sd-045` | `/docs/build/guides/dapps/frontend-guide` | 35 | `Freighter wallet requires a secure connection (HTTPS) to interact with your dapp.` | No `http://localhost` qualification |

The exact affected anchors are `#xdr-conversions-in-smart-contracts`, the pooled-accounts page root,
and `#setup-https-on-localhost`, respectively.

The initial result exceeded the response limit. Raven retained the complete result in its normal artifact path.
The root read that artifact and returned only the matched sections and boolean assertions.
Artifact ID: `103fdec7-7578-44fd-b537-c45dfac91074`; reported SHA-256 prefix: `24ace1e0f604`.
The artifact expires at `2026-09-21T21:16:57.338Z` and requires the same authenticated owner.
The table above preserves the relevant evidence after expiry.

Use this bounded query for a new verification:

```js
const paths = [
  '/docs/build/guides/conversions/address-conversions',
  '/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos',
  '/docs/build/guides/dapps/frontend-guide',
];
return await Promise.all(paths.map(async path => {
  const r = await stellarDocs.get_doc_page_sections({path, includeContent: true});
  if (!r.ok) return {path, error: r.error};
  const content = r.data.sections.map(s => s.content ?? '').join('\n');
  return {
    path,
    complete: r.data.complete,
    nbSections: r.data.nbSections,
    staleUnwrap: /Address::from_xdr\([^)]*\)\.unwrap\(\)/.test(content),
    staleMemos: content.includes('We used memos in the past'),
    staleHttps: content.includes('Freighter wallet requires a secure connection (HTTPS)'),
    correctedResult: content.includes('ConversionError'),
    correctedLoopback: content.includes('http://localhost'),
  };
}));
```

## Rendered source check

The root fetched all three corresponding `https://developers.stellar.org` pages at `21:17:36Z`.
All returned HTTP 200.
The root repeated direct HTTP reads for `sd-041` and `sd-045` at `2026-09-14T21:26:39Z`.
Both returned HTTP 200 with corrected text and without their original defective sentences.
An independent page-search read reported older text. That observation does not establish the current direct HTTP response.

| Finding | Current rendered evidence |
|---|---|
| `sd-040` | The example returns `Result<Address, ConversionError>`. The prose discusses errors from untrusted input. |
| `sd-041` | The lead says many services still rely on transaction memos. It retains support for both approaches. |
| `sd-045` | The page names `http://localhost` and `http://127.0.0.1` as secure contexts. Plain HTTP works locally. |

Sources:

- https://developers.stellar.org/docs/build/guides/conversions/address-conversions
- https://developers.stellar.org/docs/build/guides/transactions/pooled-accounts-muxed-accounts-memos
- https://developers.stellar.org/docs/build/guides/dapps/frontend-guide

## Required next check

After ingestion, repeat each original production query and confirm both corrected text and removal of defective text.
Inspect the affected records in every relevant serving index before declaring the search defect resolved.
Do not infer ingestion from a merged PR, deployment, title-count change, or aggregate crawler success.
This audit changed no crawler, index, rule, synonym, or setting.
