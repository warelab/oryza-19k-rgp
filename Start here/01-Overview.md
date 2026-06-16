---
title: A Global Atlas of 19,035 Rice Genomes
---

## Choose your path

Six entry points into the atlas — pick the task you have in mind and we'll route you to the right platform.

| I want to… | Platform |
| --- | --- |
| **Explore a gene or SNP** — genotypes, haplotypes, and allele frequencies for a region across all accessions | [SNP-Seek v3](/platforms) |
| **Browse a genome** — gene models, variants, and predicted effects in an Ensembl-based browser + REST API | [GrameneOryza](/platforms) |
| **Climate ↔ genome (G×E)** — genotype–environment associations across landraces | [Oryza CLIMtools](/platforms) |
| **Predict a trait** — pre-trained models predict agronomic traits from genotypes (Docker / Colab) | [Code & Models](/platforms) |
| **Query efficiently (API)** — stream a locus across 19,035 genomes with tabix, no full download | [API & programmatic](/api) |
| **Bulk download** — raw reads, full variant archives, and citable DOIs (NCBI / EVA / KAUST) | [Archives & Bulk](/platforms) |

## By data type

| I have / want… | Go to | How |
| --- | --- | --- |
| A gene or region of interest | [GrameneOryza](/platforms) / [SNP-Seek](/platforms) | Ensembl REST · genotype viewer |
| Genotypes for all accessions at a locus | [Remote tabix](/api) / SNP-Seek | stream the region · or precomputed table |
| An environmental / climate question | [Oryza CLIMtools](/platforms) | GenoCLIM / CLIMGeno tables |
| A phenotype to predict | [Code & Models](/platforms) | pre-trained models (Docker/Colab) |
| Bulk variants or raw reads | [Archives](/platforms) | NCBI · EVA · KAUST DOI |
| A summary, not a query | [Precomputed tables](/api) | Zenodo deposit (allele freq, benchmark, …) |

## One dataset, five access points

The 19,035 rice genomes (5 references) flow into three interactive platforms, which share files with the archives and code:

- **SNP-Seek v3** — genotypes · haplotypes · REST
- **GrameneOryza** — browser · Ensembl REST · FTP
- **Oryza CLIMtools** — climate × genome tables
- **Archives & Bulk** — NCBI · EVA · KAUST DOI
- **Code & Models** — pipelines · pre-trained models

## Quick start — two ways in

**API (curl)**

```bash
# Resolve a gene to coordinates (GrameneOryza / Ensembl REST)
curl -s "https://rest.ensembl.org/lookup/id/Os03g0752800?content-type=application/json"
# -> MADS14, chr3:31,031,753-31,041,563
```

**Python**

```python
import oryza19k as o19           # the access cookbook (notebooks/oryza19k.py)
gene = o19.lookup_gene("Os03g0752800")          # MADS14 via Ensembl REST
bench = o19.summary_table("benchmark")          # precomputed model x trait table
preds = o19.predict_trait(genotypes, "hdg_80head")   # pre-trained model
```

New here? See the [oryza19k cookbook](/api), [Ensembl REST](/api), and [trait-prediction models](/platforms). The [example workflows](/workflows) walk from a gene of interest all the way to a testable hypothesis, touching every platform.

> **Cite this resource.** Zhou Y. *et al.* Unity in Diversity: A Global Atlas of 19,035 Rice Genomes. *Cell* (in revision), CELL-D-26-01478. Full citation and data-availability details on the [Cite](/cite) page.
