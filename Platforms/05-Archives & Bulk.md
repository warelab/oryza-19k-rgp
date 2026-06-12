---
title: Archives & Bulk Data
---

**Public.** The cold-storage, citable layer: raw reads, the full variant archive, and permanent DOIs — for when you need the underlying data rather than an interactive query.

## README — accessions & what's there

| Resource | Accession / DOI | Contents |
| --- | --- | --- |
| NCBI BioProject | [PRJNA954521](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA954521) | 9K-RGP clean sequencing data |
| NCBI BioProject | [PRJNA597070](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA597070) | 3K-RGP data |
| NCBI BioProject | [PRJNA952097](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA952097) | PacBio HiFi for IR64RS2 |
| European Variation Archive | [PRJEB105137](https://www.ebi.ac.uk/eva/?eva-study=PRJEB105137) | Variants — SNP set [ERZ28769989](https://www.ebi.ac.uk/ena/browser/view/ERZ28769989), InDel set [ERZ28769990](https://www.ebi.ac.uk/ena/browser/view/ERZ28769990) |
| KAUST repository | [DOI 10.25781/N3AF-NP78](https://doi.org/10.25781/N3AF-NP78) | Raw reads (permanent handle) |

> **Use this when…** you need raw FASTQ/gVCF, the complete variant archive, or a permanent citable handle — not for interactive queries.

The EVA variant archive (PRJEB105137) is also surfaced interactively via [GrameneOryza](/platforms). For ready-made summaries instead of raw archives, see the [precomputed tables](/api).

## Tutorial — fetch from the archives

1. Locate the accession (above) at the [EVA/ENA](https://www.ebi.ac.uk/ena/browser/home) or [NCBI SRA](https://www.ncbi.nlm.nih.gov/sra).
2. Download via the archive's interface or command-line tools.
3. Verify checksums before use.

## Workflow — get a VCF, then slice it locally

Goal: get the genome-wide SNP VCF for one reference from the EVA, then slice a region locally with tabix (bridging to [efficient access](/api)). This underpins the genotype steps of [Workflow A](/workflows); the runnable notebooks are on [Resources](/resources).

## Examples

**EVA / ENA**

```bash
# Download a variant file by accession, then index for tabix
wget https://ftp.ebi.ac.uk/eva/.../19K-RGP.IRGSP-1.0.snps.vcf.gz
tabix -p vcf 19K-RGP.IRGSP-1.0.snps.vcf.gz
```

**NCBI SRA**

```bash
# Fetch raw reads for one run
prefetch SRR24065674 && fasterq-dump SRR24065674
```

## Access & cite

**Public.** Open, anonymous archive access (some records are embargoed during peer review and released at publication).

Cite the manuscript and the relevant archive accession (see [Cite](/cite)).
