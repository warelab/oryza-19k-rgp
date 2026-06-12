---
title: Workflow A — MADS14 → heading date
---

**Question:** does natural variation at *MADS14* in Xian/Indica track local temperature, and can I turn that into a testable heading-date prediction?

1. **Resolve the gene** ([GrameneOryza](/platforms) / [Ensembl REST](/api)) → `MADS14`, chr3:31,031,753–31,041,563.
2. **Variants & effects** in the locus (overlap + VEP — [Ensembl REST](/api)).
3. **Genotypes across XI** via [remote tabix](/api) (or [SNP-Seek](/platforms)).
4. **Climate association** ([Oryza CLIMtools](/platforms)) → top variable **BIO6** (min temp, coldest month).
5. **Join climate + phenotype**, reproduce the haplotype–climate signal.
6. **Predict heading date** genome-wide and rank candidates (pre-trained model — [Code & Models](/platforms)).

```python
import oryza19k as o19
gene  = o19.lookup_gene("Os03g0752800")                  # MADS14
vars  = o19.region_features("3:31031753-31041563", feature="variation")
clim  = o19.climate_for_gene("MADS14", group="XI")       # -> BIO6
preds = o19.predict_trait(genotypes, "hdg_80head")
```

The runnable notebook is `workflow_A_mads14_heading_date.py` — see [all notebooks on Resources](/resources).
