---
title: Code & Models
---

**Public.** All analysis pipelines for the paper, plus pre-trained AI models that predict agronomic traits directly from genotypes.

[Open the repository ↗](https://github.com/YongZhou2019/19K-RGP)

Repository: `github.com/YongZhou2019/19K-RGP` (MIT license). Reproducible environment via Docker; one-click Google Colab.

## README — what it is & what it hosts

The repository holds the workflows, pipelines, and scripts behind the manuscript. Variant calling uses the [HPC-GVCW](https://github.com/IBEXCluster/HPC-GVCW) pipeline (*BMC Biology*, DOI 10.1186/s12915-024-01820-5). Analysis modules:

| Module | What it does |
| --- | --- |
| `AI-drive Predictive Phenotype Modeling` | Pre-trained trait-prediction models + demos (see below) |
| `VariantCalling Scripts` | GATK4 variant calling (Phase 1–4), via HPC-GVCW |
| `GWAS scripts` | GAPIT GWAS, QC, Manhattan plots |
| `AlleleFrequency` / `RARE VARIANTS` | Allele-frequency, MAF comparison, rare-variant statistics |
| `AlphaFold` / `Molecular_dynamics` | AF2/AF3 structure modeling; MD (gyration, energy) and EVO2 mutation scoring |
| `cBasmati` (LAI) | Local-ancestry inference and F~ST~ |

The rare-variant and high-effect modules power [Workflow B](/workflows) (rare TB1/FC1 variant); the prediction model drives [Workflow A](/workflows) and [Workflow C](/workflows).

> **Use this when…** you want to predict a trait for new genotypes, reproduce a figure, or run a pipeline end-to-end.

## Tutorial — run the heading-date demo three ways

1. **Colab (one click):** open the demo notebook and run the cells top to bottom.
2. **Docker (recommended):** launch the bundled RAPIDS/PyTorch/Jupyter image (command in Examples), then open `Heading_Date_Demo.ipynb`.
3. **Python script:** `python heading_date_predictor.py` writes predictions + a distribution plot to `output/`.

> The deployed model consumes the **SHAP-selected top-1,000 SNPs** (from the 165,640-SNP core set), not the full matrix — that is what makes inference fast.

## Workflow — score the whole collection for a trait

Goal: predict heading date for the ~5,500 accessions that lack a measured value. Provide a genotype frame with an `IID`/`ID` column plus the top-1,000 SNP features; `oryza19k.predict_trait()` (the [oryza19k cookbook](/api)) aligns columns, imputes missing values with the shipped imputer, loads the model, and returns predictions. Get the core-SNP matrix from the [precomputed tables](/api) or stream regions via [remote tabix](/api). See [Workflow C](/workflows) for the full benchmarked version; the runnable notebook is on [Resources](/resources).

## Examples

**Docker**

```bash
docker run --gpus all --ipc=host --ulimit memlock=-1 --ulimit stack=67108864 --rm \
  -p 10000:8888 -p 8501:8501 -v ${PWD}:/workspace/mycode \
  abdelghafour1/ngc_tf_rapids_25_01_vscode_torch:2025-v3 \
  jupyter lab --ip=0.0.0.0 --allow-root
```

**Python**

```python
import joblib, numpy as np, pandas as pd
model   = joblib.load("best_trained_model_hdg_80head2025.pkl")
imputer = joblib.load("most_freq_imputer_hdg_80head2025.pkl")
df = pd.read_csv("input_top_1000_features.csv")          # IID, Phenotype, + 1000 SNPs
X  = df.drop(columns=["IID", "Phenotype"]).replace(-9, np.nan).values.astype("float64")
y_pred = model.predict(imputer.transform(X))
```

> Currently the **heading-date** model is public; the four remaining trait models (grain weight/length/width and length-to-width ratio) are added at resubmission.

## Access & cite

**Public.** Open on GitHub (MIT). Reproducible environment via the Docker image above; pre-trained models load with `joblib`.

Cite the manuscript (see [Cite](/cite)) and the HPC-GVCW pipeline (*BMC Biology*, 2024).
