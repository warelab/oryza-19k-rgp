---
title: Workflow B — Rare TB1/FC1 variant
---

**Question:** find carriers of the rare *TB1/FC1* promoter variant that strengthens an *OsBZR1* motif, and check the tiller-number association.

1. **Locate** *TB1/FC1* ([Ensembl](/api)) — `FC1`, chr3:28,428,504–28,430,438.
2. **Genotype the site** across the panel via [remote tabix](/api); get allele frequency ([precomputed table](/api); ≈38 carriers, 0.95%).
3. **Confirm the regulatory consequence** (VEP — [Ensembl REST](/api) — + the high-effect-variant table).
4. **Pull tiller number + group/geography** for carriers.
5. **Effect size with a 95% CI**, plus a relatedness/geography confounding check.

> With ~38 carriers, always report the confidence interval and confirm the carriers are not a single clade or locale before interpreting the effect.

The runnable notebook is `workflow_B_tb1_tiller_number.py` — see [all notebooks on Resources](/resources).
