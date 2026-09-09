# Catalog and Table Format Notes

Notes for understanding and working with catalogs and table formats, and for designing a modern data lakehouse in the cloud.

## Index

| Document | | |
|---|---|---|
| **[What a Catalog Owes You](docs/catalog-evaluation.md)** | ~50 min | Thirteen dimensions that separate a technical catalog from a table listing, each with a test and worked code. Namespaces, SQL dialects, Glue vs. Glue with Lake Formation, Glue vs. Unity Catalog vs. Horizon, Polaris scored self-hosted and Snowflake-hosted, and consolidated scores. |
| **[Where Commit Authority Lives](docs/commit-coordination.md)** | ~12 min | Why Glue can serialize Iceberg commits but not Delta ones, why S3's missing put-if-absent was a Delta problem and never an Iceberg one, and what Delta 4.1 catalog-managed tables change. |

Each document is self-contained — read either one first. `html/` holds the same two notes as standalone designed pages.
