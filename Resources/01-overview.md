---
title: Resources & downloads
---

The whole data-access package — the `oryza19k` helper and [example notebooks](/workflows), the precomputed tables, and Supplementary Note 10 — bundled into this site. Grab individual files below, or the complete package as one archive.

⬇ **Download all files (.zip)** — `downloads/19K-RGP-data-access-package.zip`

## Python — the `oryza19k` access cookbook

The client-side cookbook that orchestrates every platform (see the [API page](/api) for what it is and what it needs). `import oryza19k as o19`, then `o19.<function>(...)`.

| File | What it is |
| --- | --- |
| `oryza19k.py` | The access-cookbook helper (Ensembl REST, tabix, CLIMtools, models, summaries) |
| `requirements.txt` | Library requirements (core + optional groups) |
| `workflow_A_mads14_heading_date.py` | [Workflow A — MADS14 → heading-date hypothesis](/workflows) |
| `workflow_B_tb1_tiller_number.py` | [Workflow B — rare TB1/FC1 variant → tiller number](/workflows) |
| `workflow_C_imputation_benchmark.py` | [Workflow C — whole-collection imputation & benchmarking](/workflows) |
| `README.md` | How to run the notebooks; full `oryza19k` reference |

> The workflows are [jupytext](https://jupytext.readthedocs.io) percent-format `.py` files — valid notebook sources. Convert to `.ipynb` with `jupytext --to notebook workflow_*.py`, or run as plain scripts.

## Precomputed summary tables

DOI-citable summaries so common questions need no large query. At publication these are mirrored on Zenodo; load them in code via the [precomputed summaries API](/api).

| Table | Contents | Size |
| --- | --- | --- |
| `allele_frequency_core_snps.tsv` | 165,640 SNPs × global + per-group allele frequency | ~19 MB |
| `genomic_prediction_benchmark.tsv` | 23 models × 5 traits (Spearman, R², training time) | ~13 KB |
| `accession_passport.tsv` | accession, varietal group, #phenotypes scored | ~0.4 MB |
| `phenotypes_by_accession.tsv` | accession × 24 phenotypes (+ group) | ~1.4 MB |
| `generate_tables.py` | Reproducible generator for the tables above | ~8 KB |

## Documentation

| Document | What it is |
| --- | --- |
| Supplementary Note 10 | Data Access and Visualization (§§10.1–10.6) |
| Package README | Overview of the whole package |

> **Using the .zip:** it bundles the data-access package — the `oryza19k` cookbook and example workflows (`notebooks/`), the precomputed summary tables (`precomputed_tables/`), and Supplementary Note 10. Unzip, then `pip install -r notebooks/requirements.txt` to run the workflows, or open the tables directly in pandas/R. Start with the `README.md`.
