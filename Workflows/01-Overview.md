---
title: Example workflows
---

Three runnable, cross-platform recipes anchored to results in the paper. Each ships as a notebook (Colab / Docker) with committed outputs, and falls back to precomputed tables so it always runs.

[Notebooks on GitHub ↗](https://github.com/YongZhou2019/19K-RGP) · [Download the notebooks](/resources)

## What you need to run these

Every notebook runs top-to-bottom as-is — an internet connection covers the Ensembl steps, and the rest read the bundled `precomputed_tables/`. Any step that needs an external resource falls back to a shipped table or a short note, so nothing ever crashes. Each notebook's first cell has a per-step setup table.

Two steps unlock the full result once you have the resource (each auto-skips with a note until then):

- **Trait prediction** (`predict_trait` — workflows A & C) needs the pre-trained model: `git clone https://github.com/YongZhou2019/19K-RGP`, then pass `models_dir="…/AI-drive Predictive Phenotype Modeling"`.
- **Streaming genotypes** (`tabix` — workflows A & B) needs the public VCF host: set `o19.CONFIG.vcf_base` (credential-free at publication); otherwise it falls back to the precomputed allele-frequency table.

**Install:** `pip install pandas numpy requests` (already in Colab / the Docker image); add `pyarrow` for fast local genotype slices and `joblib scikit-learn xgboost lightgbm` only for the prediction step.

## The three workflows

- [**Workflow A** — From the MADS50/MADS14 locus to a heading-date hypothesis](/workflows)
- [**Workflow B** — A rare TB1/FC1 high-effect variant and tiller number](/workflows)
- [**Workflow C** — Whole-collection trait imputation & benchmarking](/workflows)
