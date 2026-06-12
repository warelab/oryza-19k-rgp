---
title: SNP-Seek v3
---

**Public.** IRRI's variant-and-phenotype warehouse for the rice panels — genotypes, local haplotypes, allele frequencies, and accession passport/phenotype data, all queryable for a region across every accession at once.

[Open SNP-Seek ↗](https://snp-seek.irri.org)

## README — what it is & what it hosts

The 19K-RGP release in SNP-Seek provides biallelic SNPs and small InDels (plus gVCFs) called against two references.

| Dataset | Reference | Access |
| --- | --- | --- |
| 19K-RGP SNPs + InDels | Nipponbare IRGSP-1.0 (GJ) | viewer · bulk · API |
| 19K-RGP SNPs + InDels | MH63RS3 (XI) | viewer · bulk · API |

Interactive tools: genotype viewer, embedded JBrowse, gene-locus search, pairwise SNP comparison, allele frequencies, phenotypes, and subpopulation grouping.

> **Use this when…** you want all-accession genotypes or local haplotypes for a small region (genes, QTLs < 500 kb), allele frequencies, or to tie genotype to IRRI passport/phenotype.

## Tutorial — the genotype viewer (OsMADS50)

1. Open *Search → Genotype* and enter the gene `OsMADS50` (or a region).
2. Choose the reference (e.g. IRGSP-1.0) and a variety subset (e.g. XI).
3. Render the genotype matrix; click *Compute local haplotypes* to group accessions.
4. Read off the haplotype groups and export the table.

## Workflow — genotypes + allele frequencies at a locus

Goal: get all 19K-RGP genotypes and per-group allele frequencies at *MADS14* (chr3) in XI as a table. Region-query the locus → open the allele-frequency panel → download the genotype matrix (HDF5/CSV) → load in pandas. The region pull is small (seconds). This is step 3 of [Workflow A](/workflows); the runnable notebook is on [Resources](/resources).

## Examples

> The SNP-Seek REST routes follow Mansueto *et al.* 2017; exact paths/params are being confirmed with the IRRI team (see the [SNP-Seek REST reference](/api)). Until then, the equivalent query runs via [remote tabix](/api) (VCFs served via [GrameneOryza](/platforms) FTP) or the [precomputed allele-frequency table](/api).

**curl**

```bash
# Genotype-by-region (schema per SNP-Seek II; confirm exact route with IRRI)
curl -s "https://snp-seek.irri.org/<api>/genotype?ref=IRGSP-1.0&chrom=3&start=31031753&end=31041563&varset=XI"
```

**Python**

```python
import oryza19k as o19
# Documented, credential-free alternative today: stream the region with tabix
gt = o19.region_genotypes("Chr03", 31031753, 31041563, ref="IRGSP-1.0", source="tabix")
```

## Access & cite

**Public.** Anonymous web UI and bulk downloads (no login): VCF, HDF5, genotype matrices; 3K Rice Genomes Open Data on AWS. The [REST API](/api) is login-free, but its exact paths are being confirmed with IRRI — use [remote tabix](/api) as the interim programmatic path.

Cite: Mansueto *et al.* (2017) *Nucleic Acids Research* — "SNP-Seek II"; Alexandrov *et al.* (2015) *NAR*.
