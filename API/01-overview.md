---
title: API & programmatic access
---

There is no single "unified API" — the platforms are heterogeneous. Instead we document each one's existing interface honestly, and provide a client-side cookbook (`oryza19k`) that orchestrates across them.

## Access matrix

| Platform | Programmatic method | Auth | Status |
| --- | --- | --- | --- |
| [GrameneOryza](/platforms) | Ensembl REST (`rest.ensembl.org`) · BioMart | none | Stable |
| Gramene FTP | Remote `tabix` of bgzipped VCFs | none | Standard |
| [SNP-Seek v3](/platforms) | REST (genotype / variety / SNP) | none | Confirm paths (IRRI) |
| [Oryza CLIMtools](/platforms) | Downloadable tables (no REST API) | none | Tables |
| [Code & Models](/platforms) | Git · Docker · `oryza19k.predict_trait()` | none | Open |
| Precomputed summaries | Zenodo (DOI) · `oryza19k.summary_table()` | none | At publication |

See the [oryza19k cookbook](/api), the per-endpoint references ([Ensembl REST](/api), [Remote tabix](/api)), and the [precomputed summaries](/api).
