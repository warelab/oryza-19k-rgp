---
title: The oryza19k cookbook
---

`oryza19k` is a single-file Python helper (`notebooks/oryza19k.py`) — an *access cookbook*, not a server or a new API. Each function wraps an interface that already exists, so a workflow is a few clean calls. Use it as `import oryza19k as o19`, then `o19.<function>(...)`. Download it from [Resources](/resources).

| Function | Wraps | Network? |
| --- | --- | --- |
| `lookup_gene` · `region_features` · `vep_effects` | Ensembl REST | yes |
| `region_genotypes(source="tabix")` | stream a bgzipped VCF | yes (public VCF host) |
| `climate_for_gene` · `accession_climate` | CLIMtools tables | no |
| `predict_trait` | the repo's pre-trained model | no (local model files) |
| `summary_table` | precomputed tables | no (local) / yes (Zenodo) |

## What it needs

| To use… | Libraries | Data |
| --- | --- | --- |
| Import + Ensembl + local tables | `pandas`, `numpy`, `pyarrow` (`requests` optional) | none / the precomputed `.tsv` files |
| `predict_trait` | `joblib`, `scikit-learn`, `xgboost`, `lightgbm` | a clone of the GitHub repo (model + imputer + features) |
| `region_genotypes("tabix")` | `pysam` or the `tabix` CLI | a public bgzipped + indexed VCF URL |

Environments: a minimal `pip install pandas numpy pyarrow` covers Ensembl, tabix, and the precomputed tables; **Colab** or the project **Docker** image (which bundles the ML stack) is recommended for `predict_trait`. Full list in `notebooks/requirements.txt`.

```python
import oryza19k as o19
o19.lookup_gene("Os03g0752800")                       # Ensembl REST — no extra deps
o19.summary_table("allele_freq_by_group")             # precomputed table — pandas only
o19.predict_trait(genotypes, "hdg_80head",            # the repo's pre-trained model
                  models_dir="…/AI-drive Predictive Phenotype Modeling")
```

> `predict_trait` **is your GitHub demo, wrapped**: it loads the team's own `.pkl` model + imputer and calls `model.predict()` on the SHAP-selected top-1,000 SNPs — it does not retrain or substitute a model. See [Code & Models](/platforms) and [Workflow C](/workflows).
