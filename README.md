# Catalog and Table Format Notes

Working notes on lakehouse catalogs and table formats: who arbitrates writes, who governs reads, and what any of it costs you if you want to leave later.

Each document is self-contained — read either one first.

| Document | Reading time | What it covers |
|---|---|---|
| **[What a Catalog Owes You](docs/catalog-evaluation.md)** | ~50 min (~10 min skim path) | Thirteen dimensions that separate a technical catalog from a table listing, each with a test you can run and code for both answers. Namespaces and why depth matters. The SQL-dialect problem. Glue natively vs. Glue with Lake Formation. Glue vs. Unity Catalog vs. Horizon, with Horizon broken out by table kind. Apache Polaris scored self-hosted and Snowflake-hosted, plus what self-hosting means you build. Consolidated scores. |
| **[Where Commit Authority Lives](docs/commit-coordination.md)** | ~12 min | Why Glue can serialize Iceberg commits but not Delta ones. Why S3's missing put-if-absent was a Delta problem and never an Iceberg one. What changes under Delta 4.1 catalog-managed tables. |

## The short version

**Iceberg puts its atomicity in the catalog; classic Delta puts its atomicity in the object store's filename space.** Almost every asymmetry between the two — which catalogs can coordinate which format, why S3's conditional-write gap hurt one and not the other, why Glue is a real catalog for one and a directory listing for the other — falls out of that single difference.

For the evaluation: score **D2 (commit authority) first**, for the format you actually write. It is a gate, not one point among thirteen. Only compare totals among the candidates that pass it.

## Scope

These notes evaluate the *technical* catalog. They deliberately exclude the semantic and AI layer — metric and semantic views, natural-language query, agent context and retrieval, and the assistant features Databricks and Snowflake sell alongside their catalogs. That is a different product category with different competitors, and it moves fast enough to date any comparison within months.

The exclusion is not a claim that the layers are unrelated: whatever semantic layer you adopt later reads descriptions, tags, constraints, lineage and query history *out of* the catalog, which is D7 and D9 and is scored. And it is a snapshot — semantic views are being moved into these catalogs as first-class objects, which will make them a D9 question before long.

## Repository layout

```
docs/     Markdown — canonical. Renders on GitHub, diffs cleanly in review.
html/     The same notes as designed, standalone HTML pages. GitHub shows
          these as source; open them locally, or enable GitHub Pages.
```

**Why Markdown is canonical:** GitHub does not render `.html` in its web UI, so an HTML-only repo is unreadable in the place people open it. Markdown renders inline, diffs meaningfully in pull requests — which matters for a document a team will argue with — is greppable, and GitHub renders the Mermaid diagrams natively.

To serve the HTML versions: **Settings → Pages → Deploy from a branch → `main` / root**, then open `/html/catalog-evaluation.html`.

## Reviewed against

Delta 4.1–4.3 · Unity Catalog OSS 0.4 · Apache Polaris 1.x · AWS Glue and Lake Formation · Snowflake Horizon and Open Catalog — as of September 2026.

Scores are judgement calls for platform planning, not benchmarks. Delta support across this ecosystem is moving quickly; verify D2 against current releases rather than against a comparison table, including these.
