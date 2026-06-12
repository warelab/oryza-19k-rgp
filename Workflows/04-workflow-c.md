---
title: Workflow C — Imputation & benchmark
---

**Question:** I have genotypes for accessions with no measured grain weight — predict it, and show the method's standing against GBLUP.

1. **Get the core-SNP matrix** ([precomputed table](/api) or stream regions via [tabix](/api)).
2. **Load a pre-trained model** ([Code & Models](/platforms)) and predict on the missing set.
3. **Benchmark** against rrBLUP / GBLUP / BayesA–C and tabular deep models.
4. **Interpret** via the SHAP-top-SNP → gene table ([precomputed](/api)).

```python
import oryza19k as o19
bench = o19.summary_table("benchmark")                   # 23 models x 5 traits
bench[bench["trait"] == "Heading date"].sort_values("spearman", ascending=False).head()
#  CatBoost 0.838 · XGBoost 0.837 · RandomForest 0.834 · LightGBM 0.833 · GBLUP 0.830
```

The runnable notebook is `workflow_C_imputation_benchmark.py` — see [all notebooks on Resources](/resources).
