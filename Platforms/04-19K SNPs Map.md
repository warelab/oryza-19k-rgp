---
title: 19K SNPs Map
---

**Public.** Interactive climate ↔ genome (G×E) association apps over the rice landrace collection — explore which environmental variables track natural genetic variation.

[Open Oryza CLIMtools ↗](https://www.gramene.org/CLIMtools/oryza_19K-RGP)

## README — what it is & what it hosts

Three R/Shiny applications:

| App | Answers |
| --- | --- |
| **OryzaCLIM** | What is each accession's local environment? (per-accession geo-environmental variables) |
| **Oryza GenoCLIM** | Which climate variables associate with my gene? |
| **Oryza CLIMGeno** | Which genotypes associate with an environmental variable? |

> CLIMtools has **no REST API**. The supported programmatic path is its **downloadable result tables** (read in pandas/R) — see [CLIMtools in the API reference](/api); the application source is on GitHub (Apache 2.0).

## Tutorial — GenoCLIM (MADS14 / MADS50)

1. Open *Oryza GenoCLIM* and enter a gene (e.g. `MADS14`).
2. Read the ranked climate-association profile; the top variable is **BIO6** (minimum temperature of the coldest month).
3. Download the association table.
4. In *OryzaCLIM*, enter an accession to view its full geo-environmental vector.

## Workflow — a gene's top climate driver, then test it

Goal: get the climate variable most associated with heading date for a candidate gene, and the per-accession climate to test it. GenoCLIM gene query → download table → join OryzaCLIM/CLIMGeno per-accession climate to the phenotype. See [Workflow A](/workflows); the runnable notebook is on [Resources](/resources).

## Examples

Export the table from GenoCLIM, or use the [bundled tables](/resources) / [precomputed summaries](/api).

**Python**

```python
import pandas as pd
genoclim = pd.read_csv("climtools_genoclim.tsv", sep="\t")   # exported / precomputed table
mads14 = genoclim[genoclim["gene"].str.contains("MADS14", case=False)]
mads14.sort_values("P").head()                                # top variable: BIO6
```

**R**

```r
genoclim <- read.csv("climtools_genoclim.tsv", sep = "\t")
subset(genoclim, grepl("MADS14", gene, ignore.case = TRUE))
```

## Access & cite

**Public.** Interactive web apps + downloadable tables; no login. Source: [github.com/CLIMtools](https://github.com/CLIMtools) (Apache 2.0).

Cite: Ferrero-Serrano *et al.* (2024) *Plant Communications* — Oryza CLIMtools.
