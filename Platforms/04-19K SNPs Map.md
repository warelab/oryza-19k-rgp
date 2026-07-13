---
title: 19K SNPs Map
---

**Public.** A Nipponbare-based genome browser for exploring SNP density, AC/MAF-defined variant classes, gene context, and carrier subgroups across the 19K-RGP collection.

[Open 19K SNPs Map ↗](https://riceome.hzau.edu.cn/19k/)

## README — what it is & what it hosts

19K SNPs Map displays variants across the 12 Nipponbare IRGSP-1.0 chromosomes, together with genome annotations and a 116-gene core set for breeding research.

| View | What it shows |
| --- | --- |
| **SNP density** | Chromosome-scale density for ultra-rare, rare, low-frequency, and common SNPs on a shared log scale |
| **SNP sites** | Position, REF/ALT, allele count (AC), allele number (AN), and minor allele frequency (MAF) after zooming into a region |
| **Genes** | All annotated genes plus the 116-gene core breeding set; search by gene ID, name, transcript, exon, or other annotation |
| **SNP detail** | Carrier count, homozygous-ALT count, subgroup summary, and paginated carrier samples when sample-level data are available |
| **Gene detail** | Transcript structure, feature annotations, and SNP counts in the gene body and its upstream/downstream 2 kb regions |

The study divides standing variants into four categories, using slightly modified thresholds from human genetics:

- **Ultra-rare:** `AC ≤ 10`
- **Rare:** `AC > 10` and `MAF ≤ 0.01`
- **Low-frequency:** `0.01 < MAF ≤ 0.05`
- **Common:** `MAF > 0.05`

> **Use this when…** you want to locate SNPs from the four AC/MAF-defined classes around a candidate gene, compare their genomic density, or identify the carrier subgroups and accessions for a particular site. Use [SNP-Seek v3](/platforms) for an all-accession genotype matrix or local haplotypes, and [Gramene Oryza](/platforms) for predicted variant effects and broader comparative annotation.

## Tutorial — inspect rare variation around GS3

1. Open 19K SNPs Map and search for `GS3` under **Gene or annotation**.
2. Select `GS3 | Os03g0407400`; the browser moves to the gene and its 2 kb flanks on chromosome 3.
3. Toggle the four SNP classes and use drag-to-zoom or pan mode to inspect individual sites. If the marker limit is reached, zoom in again.
4. Open the rare SNP `Chr03_16729853_G_T`. Its detail page reports `AC = 51`, `MAF = 0.00168239`, and 26 carrier accessions, meeting the rare-variant criteria of `AC > 10` and `MAF ≤ 0.01`.
5. Read the subgroup summary: 21 carriers are GJ_trop, three are cAus, one is cBasmati, and one is XI_indica. Use the carrier table to retrieve individual sample IDs.
6. Return to the browser and open the GS3 gene marker to compare SNP counts in the upstream 2 kb, gene body, and downstream 2 kb, and to inspect the transcript model.

## Workflow — candidate gene to carrier subgroups

Goal: find variants from the four AC/MAF-defined classes near a candidate gene and identify the rice groups that carry a selected allele. Search the gene or annotation → focus its locus → compare the four density/site tracks → open a SNP → inspect AC, AN, MAF, carrier count, and subgroup distribution → retrieve carrier sample IDs from the table or JSON endpoint.

This workflow is intended for locus-scale exploration. For genotypes across every accession or haplotype analysis, continue in [SNP-Seek v3](/platforms).

## Examples

The browser uses public JSON endpoints under `/19k/api`. They are useful for reproducible queries, but are not currently advertised as a versioned long-term API.

**curl**

```bash
# Resolve a gene name or annotation to its Nipponbare locus
curl -s "https://riceome.hzau.edu.cn/19k/api/gene-search?q=GS3&limit=5"

# List rare SNPs in the first 1 kb of the GS3 gene
curl -s "https://riceome.hzau.edu.cn/19k/api/snps?chr=3&start=16729501&end=16730500&types=rare&limit=1000"

# Retrieve one SNP and its carrier/subgroup summary
curl -s "https://riceome.hzau.edu.cn/19k/api/snps/rare/Chr03_16729853_G_T"

# Page through the carrier accessions
curl -s "https://riceome.hzau.edu.cn/19k/api/snps/rare/Chr03_16729853_G_T/carriers?offset=0&limit=100"
```

**Python**

```python
import requests

base = "https://riceome.hzau.edu.cn/19k/api"
snps = requests.get(
    f"{base}/snps",
    params={
        "chr": 3,
        "start": 16_729_501,
        "end": 16_730_500,
        "types": "ultra_rare,rare,low_frequency,common",
        "limit": 1000,
    },
    timeout=30,
).json()["data"]

detail = requests.get(
    f"{base}/snps/rare/Chr03_16729853_G_T",
    timeout=30,
).json()["data"]

print(len(snps), detail["maf"], detail["subgroupCounts"])
```

SNP point queries are limited to windows of 5 Mb or less. Carrier results are paginated; common-SNP aggregate carrier statistics are available, but individual common-SNP carrier rows may not be loaded.

## Access & cite

**Public.** The web interface and JSON endpoints are anonymous and require no login. The current site is based on the Nipponbare reference and complements the multi-reference genotype, annotation, and archive resources described elsewhere in this guide.

Cite: Zhou Y., Ferrero-Serrano Á., Hsieh J.-W. A., *et al.* **Unity in Diversity: A Global Atlas of 19,035 Rice Genomes.** *Cell* (in revision), manuscript CELL-D-26-01478.
