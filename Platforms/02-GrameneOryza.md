---
title: Gramene Oryza
---

**Review.** An integrated gene search interface, Ensembl-based genome browser, and FTP site serving the 19K-RGP across all five references — with the stable Ensembl REST API for gene, region, variant-effect, and sequence queries.

[Open Gramene Oryza ↗](/gramene)


## README

The [FTP site](https://ftp.gramene.org/oryza/19K-RGP/) holds the per-reference variant calls and their predicted effects; the [Ensembl browser](http://oryza-ensembl-dev.gramene.org/index.html) visualizes them on the location, gene, and variation pages. Because Gramene Oryza is built on Ensembl, the **Ensembl REST API** `(rest.ensembl.org)` gives documented, stable access for *Oryza sativa* — see the [Ensembl REST reference](https://data.gramene.org/pansite-ensembl-108).

> **Use this when…** you need gene models, the predicted consequence of a variant (VEP), cross-reference coordinates, or to stream a VCF slice via a track hub / [remote tabix](/api).

## Tutorial

1. From the *location* page, search `OsMADS50` to reach its *gene* page.
2. Open the *variation* page and enable the 19K-RGP variation track.
3. Click a variant to inspect its predicted effect.

A video walkthrough is available at [oryza.gramene.org/videotutorials](https://oryza.gramene.org/videotutorials).

## Workflow

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
