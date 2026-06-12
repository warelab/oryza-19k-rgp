---
title: Precomputed summaries
---

A DOI-citable Zenodo deposit (mirrored on the Gramene FTP and the KAUST repository), so the most common questions need no large query. Download the tables from [Resources](/resources); used in [Workflow C](/workflows).

| Table | Contents | Format |
| --- | --- | --- |
| Allele frequencies (core SNPs) | 165,640 SNPs × global + per-group frequency | TSV |
| Accession passport | accession, varietal group, #phenotypes scored | TSV |
| Phenotypes | accession × 24 traits | TSV |
| Genomic-prediction benchmark | 23 models × 5 traits (Spearman, R², time) | TSV |
| Per-gene variant summary · HEV · GEA hits · SHAP→gene · haplotypes | exported by the platform teams | TSV |

```python
import oryza19k as o19
af = o19.summary_table("allele_freq_by_group")     # per-group allele frequencies
bm = o19.summary_table("benchmark")                # model x trait benchmark
```
