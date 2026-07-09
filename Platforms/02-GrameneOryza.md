---
title: Gramene Oryza
---

An integrated gene search interface, Ensembl-based genome browser, and FTP site serving the 19K-RGP across all five references.

[Open Gramene Oryza ↗](/gramene)


## README — what it is & what it hosts

The [FTP site](https://ftp.gramene.org/oryza/19K-RGP/) holds the per-reference variant calls and their predicted effects; the [Ensembl browser](http://oryza-ensembl-dev.gramene.org/index.html) visualizes them on the location, gene, and variation pages. Because Gramene Oryza is built on Ensembl, the **Ensembl REST API** `(rest.ensembl.org)` gives documented, stable access for *Oryza sativa* — see the [Ensembl REST reference](https://data.gramene.org/pansite-ensembl-108).

The 19K-RGP is hosted against all five platinum references, one per major *Oryza sativa* subpopulation:

| Reference | Subpopulation | Assembly |
| --- | --- | --- |
| Nipponbare | Japonica (GJ) | IRGSP-1.0 |
| IR64 | indica (XI) | IR64RS2 |
| Minghui 63 | indica (XI) | MH63RS3 |
| N22 | aus | *to confirm* |
| ARC 10497 | aromatic (Basmati) | *to confirm* |

For each reference, Gramene Oryza serves the genome assembly, gene models and annotation, and the 19K-RGP variation track (SNPs + InDels with predicted effects).

Interactive tools: region/location view; gene pages (models, transcripts, cross-references); comparative genomics (gene trees / orthologs); Plant Reactome pathway links; AlphaFold3 protein-structure models; the variation page with the 19K-RGP track and per-variant VEP; BLAST sequence search; plus track-hub streaming and FTP bulk download.

> **Use this when…** you need gene models, the predicted consequence of a variant (VEP), cross-reference coordinates, comparative genomics or pathway context, a protein structure, or to stream a VCF slice via a track hub / [remote tabix](/api).

## Tutorial — the genome browser (OsMADS50)

1. From the *location* page, search `OsMADS50` to reach its *gene* page — gene models, transcripts, and cross-references.
2. From the gene page, explore comparative genomics (gene tree / orthologs) and the linked Plant Reactome pathways.
3. Open the AlphaFold3 structure for the protein.
4. Open the *variation* page, enable the 19K-RGP variation track, and click a variant to inspect its predicted effect (VEP).
5. To locate a sequence rather than a gene name, run BLAST against a reference to jump to the region.

A video walkthrough is available at [oryza.gramene.org/videotutorials](https://oryza.gramene.org/videotutorials).

## Workflow — a locus' variants and predicted effects via REST

Goal: for *MADS14* (`Os03g0752800`), pull the gene model, all overlapping variants, and their predicted consequences. `lookup/id` → `overlap/region` (feature=variation) → `vep` → a tidy variant×consequence table. See [Workflow A](/workflows); the runnable notebook is on [Resources](/resources).

## Examples

**curl**

```bash
# Gene -> coordinates
curl -s "https://data.gramene.org/pansite-ensembl-108/lookup/id/Os03g0752800?content-type=application/json"
# Variants overlapping the locus
curl -s "https://data.gramene.org/pansite-ensembl-108/overlap/region/oryza_sativa/3:31031753-31041563?feature=variation;content-type=application/json"
# Predicted consequence (region/<chrom>:<start>-<end>/<alt>)
curl -s "https://rest.ensembl.org/vep/oryza_sativa/region/3:31037240-31037240/A?content-type=application/json"
```


## Access & cite

The [Ensembl REST API](/api) (`rest.ensembl.org`) is **public and stable now**, no login. **Review** applies only to the browser/FTP during peer review: the 19K-RGP rice resources are now live at [oryza19k.gramene.org](https://oryza19k.gramene.org) (reviewer credentials provided to the editor), moving to public, login-free production endpoints at publication. The durable variant archive is the [European Variation Archive (PRJEB105137)](https://www.ebi.ac.uk/eva/?eva-study=PRJEB105137), also documented under [Archives](/platforms).

Cite: Tello-Ruiz *et al.* (Gramene, *NAR*); the GrameneOryza database paper; the Ensembl REST API.
