---
title: Endpoints — Ensembl, SNP-Seek, tabix, CLIMtools
---

## Ensembl REST (GrameneOryza) — stable

Documented, login-free access for *Oryza sativa* gene, region, variant-effect, and sequence queries. Verified live. See [GrameneOryza](/platforms) and [Workflow A](/workflows), which uses these calls.

```bash
curl -s "https://rest.ensembl.org/lookup/id/Os03g0752800?content-type=application/json"
curl -s "https://rest.ensembl.org/overlap/region/oryza_sativa/3:31031753-31041563?feature=gene;feature=variation;content-type=application/json"
curl -s "https://rest.ensembl.org/vep/oryza_sativa/region/3:31037240-31037240/A?content-type=application/json"
curl -s "https://rest.ensembl.org/sequence/id/Os03t0752800?type=genomic;content-type=application/json"
```

## SNP-Seek REST

Genotype-by-region, variety, and SNP queries follow the SNP-Seek II design (Mansueto *et al.* 2017). See [SNP-Seek v3](/platforms).

> Exact endpoint paths/params are being confirmed with the IRRI team. Until then, prefer remote tabix (below) or the [precomputed allele-frequency table](/api) for an equivalent, credential-free query.

## Remote tabix — query 19,035 genomes without downloading them

The single most efficient access technique: the per-reference VCFs are bgzip-compressed and tabix-indexed, so any locus can be streamed over HTTPS. Demonstrated in [Workflow A](/workflows) and [Workflow B](/workflows).

**tabix / bcftools**

```bash
tabix -h https://<public-host>/19K-RGP/IRGSP-1.0/19K-RGP.IRGSP-1.0.snps.vcf.gz 3:31031753-31041563
bcftools view -r 3:31031753-31041563 https://<host>/.../19K-RGP.IRGSP-1.0.snps.vcf.gz \
  | bcftools query -f '%CHROM\t%POS\t%REF\t%ALT[\t%GT]\n'
```

**pysam**

```python
import pysam
vcf = pysam.VariantFile("https://<host>/.../19K-RGP.IRGSP-1.0.snps.vcf.gz")
for rec in vcf.fetch("3", 31031753, 31041563):
    print(rec.chrom, rec.pos, rec.ref, rec.alts)
```

> Requires the VCFs to be served with HTTP range support; the one-time `bgzip`/`tabix` preparation is coordinated with the Gramene team.

## Oryza CLIMtools — tables (no REST API)

CLIMtools is an R/Shiny resource; the supported programmatic path is its downloadable result tables, read directly in pandas/R. See the [CLIMtools examples](/platforms); used in [Workflow A](/workflows).
